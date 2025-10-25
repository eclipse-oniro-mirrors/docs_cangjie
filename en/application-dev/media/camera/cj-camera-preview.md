# Preview (Cangjie)

When developing a camera application, you need to first refer to the [Development Preparation](./cj-camera-preparation.md) to apply for relevant permissions.

The preview is the live view displayed after launching the camera, typically executed before taking photos or recording videos.

## Development Steps

For detailed API documentation, please refer to the [Camera API Reference](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md).

1. Import the camera interface, which provides camera-related properties and methods. The import method is as follows:

    <!-- compile -->

    ```cangjie
    import kit.CameraKit.*
    import ohos.hilog.Hilog
    import ohos.callback_invoke.Callback0Argument
    import ohos.business_exception.BusinessException
    ```

2. Create a Surface.

    The XComponent provides the Surface for the preview stream, while the XComponent's capabilities are provided by the UI.

    > **Note:**
    >
    > The aspect ratio of the preview stream resolution must match that of the video output stream. If the Surface display area aspect ratio in the XComponent is set to 1920:1080 (16:9), then the preview stream resolution must also maintain a 16:9 aspect ratio, such as 640:360, 960:540, or 1920:1080, and so on.

3. Use the `previewProfiles` property in the [CameraOutputCapability](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#struct-cameraoutputcapability) class to obtain the device's supported preview capabilities, which returns a `previewProfilesArray`. Then create a preview output stream using the [createPreviewOutput](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-createpreviewoutputprofile-string) method. The two parameters for this method are the first item in the `previewProfilesArray` and the `surfaceId` obtained in Step 2.

    <!-- compile -->

    ```cangjie
    func getPreviewOutput(cameraManager: CameraManager, cameraOutputCapability: CameraOutputCapability, surfaceId: String): PreviewOutput {
        let previewProfilesArray: Array<Profile> = cameraOutputCapability.previewProfiles
        let previewOutput: PreviewOutput = cameraManager.createPreviewOutput(previewProfilesArray[0], surfaceId)
        return previewOutput
    }
    ```

4. Enable the preview. Use the [Session.start](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-start) method to output the preview stream. If the API call fails, it will return an error code. For error code types, refer to [Camera Error Codes](../../../../en/application-dev/reference/CameraKit/cj-errorcode-multimedia-camera.md).

    <!-- compile -->

    ```cangjie
    func startPreviewOutput(cameraManager: CameraManager, previewOutput: PreviewOutput): Unit {
        let cameraArray: Array<CameraDevice> = cameraManager.getSupportedCameras()
        if (cameraArray.size == 0) {
            Hilog.error(0,"",'no camera.')
            return
        }
        // Get supported scene modes.
        let sceneModes: Array<SceneMode> = cameraManager.getSupportedSceneModes(cameraArray[0])
        let isSupportPhotoMode: Bool = sceneModes.indexOf(SceneMode.NormalPhoto).isSome()
        if (!isSupportPhotoMode) {
            Hilog.error(0,"",'photo mode not support')
            return
        }
        let cameraInput: CameraInput = cameraManager.createCameraInput(cameraArray[0])
        // Open the camera.
        cameraInput.open()
        let session: PhotoSession = (cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession).getOrThrow()
        session.beginConfig()
        session.addInput(cameraInput)
        session.addOutput(previewOutput)
        session.commitConfig()
        session.start()
    }
    ```

## State Monitoring

During camera application development, you can monitor the preview output stream status at any time, including preview stream start, preview stream end, and preview stream output errors.

- Register a fixed `frameStart` callback function to monitor the preview start result. This can be monitored once the `previewOutput` is successfully created. It triggers upon the first exposure of the preview, and receiving this event indicates the preview stream has started.

    <!-- compile -->

    ```cangjie
    class FrameStartCallBack <: Callback0Argument {
        public open func invoke(error:?BusinessException): Unit {
            Hilog.info(0,"","Preview frame started")
        }
    }

    func onPreviewOutputFrameStart(previewOutput: PreviewOutput): Unit {
        previewOutput.on(CameraEvents.FrameStart, FrameStartCallBack())
    }
    ```

- Register a fixed `frameEnd` callback function to monitor the preview end result. This can be monitored once the `previewOutput` is successfully created. It triggers upon the completion of the last frame, and receiving this event indicates the preview stream has ended.

    <!-- compile -->

    ```cangjie
    class FrameEndCallBack <: Callback0Argument {
        public open func invoke(error:?BusinessException): Unit {
            Hilog.info(0,"","Preview frame ended")
        }
    }

    func onPreviewOutputFrameEnd(previewOutput: PreviewOutput): Unit {
        previewOutput.on(CameraEvents.FrameEnd, FrameEndCallBack())
    }
    ```

- Register a fixed `error` callback function to monitor preview output errors. The callback returns the corresponding error code when an error occurs in the preview output API. For error code types, refer to [Camera Error Codes](../../../../en/application-dev/reference/CameraKit/cj-errorcode-multimedia-camera.md).

    <!-- compile -->

    ```cangjie
    class ErrorCallBack <: Callback0Argument {
        public open func invoke(error:?BusinessException): Unit {
            if (let Some(e) <- error) {
                Hilog.error(0,"","Preview output error code: ${e.code}","")
            }
        }
    }

    func onPreviewOutputError(previewOutput: PreviewOutput): Unit {
        previewOutput.on(CameraEvents.CameraError, ErrorCallBack())
    }
    ```