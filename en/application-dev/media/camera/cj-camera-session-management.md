# Session Management (Cangjie)

Before using camera functionalities such as preview, photo capture, video recording, or metadata, a camera session must be created.

Within a session, the following functionalities can be achieved:

- Configure camera input and output streams. The camera must complete input and output stream configuration before shooting.
  Configuring the input stream involves adding device input, which for users means selecting a specific camera device for shooting. Configuring the output stream determines the form in which data will be output. When an application needs to implement photo capture, the output stream should be configured as a preview stream and a photo capture stream. The preview stream data will be displayed on the XComponent, while the photo capture stream data will be saved to the album via the ImageReceiver interface.

- Add configurations such as flash and focus adjustment. For specific supported configurations and interface descriptions, refer to the [Camera API Reference](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md).

- Session switching control. Applications can switch camera modes by removing and adding output streams. For example, if the current session's output stream is a photo capture stream, the application can remove the photo capture stream and add a video stream as the output stream, thereby switching from photo capture to video recording.

After completing session configuration, the application can submit and start the session to begin calling camera-related functionalities.

## Development Steps

1. Import relevant interfaces as follows:

    <!-- compile -->

    ```cangjie
    import kit.CameraKit.*
    import ohos.business_exception.BusinessException
    import ohos.hilog.Hilog

    ```

2. Call the [createSession](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-createsessionscenemode) method in the cameraManager class to create a session.

    <!-- compile -->

    ```cangjie
    func getSession(cameraManager: CameraManager): Session {
        let session = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
        return session.getOrThrow()
    }
    ```

3. Call the [beginConfig](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-beginconfig) method in the PhotoSession class to configure the session.

    <!-- compile -->

    ```cangjie
    func beginConfig(photoSession: PhotoSession): Unit {
        try {
            photoSession.beginConfig()
        } catch (error: BusinessException) {
            Hilog.error(0,"","Failed to beginConfig. error: ${error.message}")
        }
    }

    ```

4. Enable the session. Add camera input and output streams to the session. Call [addInput](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-addinputcamerainput) to add the camera input stream and [addOutput](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-addoutputcameraoutput) to add the camera output stream. The following example code demonstrates adding a preview stream (previewOutput) and a photo capture stream (photoOutput), meaning the current mode supports both photo capture and preview.

    Call the [commitConfig](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-commitconfig) and [start](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-start) methods in the PhotoSession class to submit the configuration and start the session.

    <!-- compile -->

    ```cangjie
    func startSession(photoSession: PhotoSession, cameraInput: CameraInput, previewOutput: PreviewOutput, photoOutput: PhotoOutput): Unit {
        try {
            photoSession.addInput(cameraInput)
        } catch (error: BusinessException) {
            Hilog.error(0,"","Failed to addInput. error: ${error.message}")
        }
        try {
            photoSession.addOutput(previewOutput)
        } catch (error: BusinessException) {
            Hilog.error(0,"","Failed to add previewOutput. error: ${error.message}")
        }
        try {
            photoSession.addOutput(photoOutput)
        } catch (error: BusinessException) {
            Hilog.error(0,"","Failed to add photoOutput. error: ${error.message}")
        }
        try {
            photoSession.commitConfig()
        } catch (error: BusinessException) {
            Hilog.error(0,"","Failed to commitConfig. error: ${error.message}")
        }

        try {
            photoSession.start()
        } catch (error: BusinessException) {
            Hilog.error(0,"","Failed to start. error: ${error.message}")
        }
    }
    ```

5. Session control. Call the [stop](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-stop) method in the PhotoSession class to stop the current session. Call [removeOutput](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-removeoutputcameraoutput) and [addOutput](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-addoutputcameraoutput) to achieve session switching control. The following example code demonstrates removing the photo capture stream (photoOutput) and adding a video stream (videoOutput), thereby switching from photo capture to video recording.

    <!-- compile -->

    ```cangjie
    func switchOutput(photoSession: PhotoSession, videoOutput: VideoOutput, photoOutput: PhotoOutput): Unit {
    try {
        photoSession.stop()
    } catch (error: BusinessException) {
        Hilog.error(0,"","Failed to stop. error: ${error.message}")
    }

    try {
        photoSession.beginConfig()
    } catch (error: BusinessException) {
        Hilog.error(0,"","Failed to beginConfig. error: ${error.message}")
    }
    // Remove the photo capture output stream from the session.
    try {
        photoSession.removeOutput(photoOutput)
    } catch (error: BusinessException) {
        Hilog.error(0,"","Failed to remove photoOutput. error: ${error.message}")
    }
    // Add the video output stream to the session.
    try {
        photoSession.addOutput(videoOutput)
    } catch (error: BusinessException) {
        Hilog.error(0,"","Failed to add videoOutput. error: ${error.message}")
    }

}
    ```