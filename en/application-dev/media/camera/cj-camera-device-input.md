# Device Input (Cangjie)

When developing a camera application, you need to first refer to the development preparation [Apply for Relevant Permissions](./cj-camera-preparation.md).

The camera application can perform basic operations such as preview, photo capture, and video recording by invoking and controlling camera devices.

## Development Steps

For detailed API specifications, refer to the [Camera API Reference](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md).

1. Import the camera interface, which provides camera-related properties and methods. The import method is as follows:

    <!-- compile -->

    ```cangjie
    import kit.CameraKit.*
    import ohos.business_exception.BusinessException
    import ohos.hilog.Hilog
    import ohos.callback_invoke.Callback0Argument
    ```

    > **Note:**
    >
    > Camera device management must be completed before camera device input. For detailed development steps, refer to [Camera Management](./cj-camera-device-management.md).

2. Create a camera input stream using the [createCameraInput](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-createcamerainputcameradevice) method in the [CameraManager](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#class-cameramanager) class.

    <!-- compile -->

    ```cangjie
    class ErrorCallBack <: Callback0Argument {
        public open func invoke(error:?BusinessException): Unit {
            if (let Some(e) <- error) {
                Hilog.error(0,"","Camera input error code: ${e.code}","")
            }

        }
    }

    func createInput(cameraDevice: CameraDevice, cameraManager: CameraManager): CameraInput {
        // Create a camera input stream.
        let cameraInput: CameraInput = cameraManager.createCameraInput(cameraDevice)
        // Listen for cameraInput error messages.
        cameraInput.on(CameraEvents.CameraError, cameraDevice, ErrorCallBack())
        // Open the camera.
        cameraInput.open()
        return cameraInput
    }
    ```

3. Use the [getSupportedSceneModes](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-getsupportedscenemodescameradevice) method to obtain the list of modes supported by the current camera device. The list contains all supported [SceneMode](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#enum-scenemode) values.

    <!-- compile -->

    ```cangjie
    func getSupportedSceneMode(cameraDevice: CameraDevice, cameraManager: CameraManager): Array<SceneMode> {
    // Get the list of modes supported by the camera device.
        let sceneModeArray: Array<SceneMode> = cameraManager.getSupportedSceneModes(cameraDevice)
        if (sceneModeArray.size > 0) {
            for (index in 0..sceneModeArray.size) {
                Hilog.info(0,"","Camera SceneMode : ${sceneModeArray[index]}")
            }
            return sceneModeArray
        } else {
            Hilog.error(0,"","cameraManager.getSupportedSceneModes error")
            return []
        }
    }
    ```

4. Use the [getSupportedOutputCapability](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-getsupportedoutputcapabilitycameradevice-scenemode) method to obtain all output streams supported by the current camera device, such as preview streams, photo capture streams, and video recording streams. The output streams are contained in various profile fields of [CameraOutputCapability](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#class-cameraoutputcapability). Depending on the specified [SceneMode](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#enum-scenemode) of the camera device, different types of output streams need to be added.

    <!-- compile -->

    ```cangjie
    func getSupportedOutputCapability(cameraDevice: CameraDevice, cameraManager: CameraManager, sceneMode: SceneMode): CameraOutputCapability {
        // Get the output stream capabilities supported by the camera device.
        let cameraOutputCapability: CameraOutputCapability = cameraManager.getSupportedOutputCapability(cameraDevice, sceneMode)
        // Taking NormalPhoto mode as an example, preview streams and photo capture streams need to be added.
        // The previewProfiles property retrieves the preview output streams supported by the current device.
        let previewProfilesArray: Array<Profile> = cameraOutputCapability.previewProfiles
        if (!previewProfilesArray.size == 0) {
            Hilog.error(0,"","createOutput previewProfilesArray is empty")
        }
        // The photoProfiles property retrieves the photo capture output streams supported by the current device.
        let photoProfilesArray: Array<Profile> = cameraOutputCapability.photoProfiles
        if (photoProfilesArray.size == 0) {
            Hilog.error(0,"","createOutput photoProfilesArray is empty")
        }
        return cameraOutputCapability
    }
    ```