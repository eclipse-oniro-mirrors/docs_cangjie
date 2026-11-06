# Camera Metadata (Cangjie)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Before developing a camera application, you need to [apply for the related permissions](cj-camera-preparation.md).

Metadata describes the image information returned by the camera and provides its context. It provides more detailed data about the image information, such as the coordinates of the framing box of a recognized portrait in a photo or video.

Metadata uses a TAG (key) to find the corresponding data, and is used to pass parameters and configuration information, reducing memory copy operations.

## When to Use

Detect faces in an image and return high-precision face rectangle coordinates. Based on the face positioning result, the application can flexibly integrate post-processing algorithms and apply them to diverse scenarios.

## How to Develop

For details about the APIs, see [Camera API Reference](../../reference/CameraKit/cj-apis-multimedia-camera.md).

1. Import the related modules as follows.

    <!-- compile -->

    ```cangjie
    import kit.CameraKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. Obtain the metadata types supported by the current device through the [supportedMetadataObjectTypes](../../reference/CameraKit/cj-apis-multimedia-camera.md#let-supportedmetadataobjecttypes) property in [CameraOutputCapability](../../reference/CameraKit/cj-apis-multimedia-camera.md#class-cameraoutputcapability), and create the metadata output stream through the [createMetadataOutput](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-createmetadataoutputarraymetadataobjecttype) method.

    <!-- compile -->

    ```cangjie
    func getMetadataOutput(cameraManager: CameraManager, cameraOutputCapability: CameraOutputCapability): MetadataOutput {
        let metadataObjectTypes: Array<MetadataObjectType> = cameraOutputCapability.supportedMetadataObjectTypes
        let metadataOutput = cameraManager.createMetadataOutput(metadataObjectTypes)
        return metadataOutput
    }
    ```

3. Configure the session. Add the camera input stream and metadata output stream to the session, call [commitConfig](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-commitconfig) and [start](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-start) to commit the configuration, and start the session.

    For details about how to obtain the device input (cameraInput) and preview output (previewOutput), see [Device Input](cj-camera-device-input.md#development-steps) and [Camera Preview Development Steps](cj-camera-device-input.md).

    <!-- compile -->

    ```cangjie
    func startMetadataOutput(photoSession: PhotoSession, cameraInput: CameraInput, previewOutput: PreviewOutput,
        metadataOutput: MetadataOutput): Unit {
        try {
            photoSession.beginConfig()
            photoSession.addInput(cameraInput)
            photoSession.addOutput(previewOutput)
            photoSession.addOutput(metadataOutput)
            photoSession.commitConfig()
            photoSession.start()
        } catch (e: BusinessException) {
            Hilog.error(0, "test", "startMetadataOutput call failed: ${e.message}")
        }
    }
    ```

4. Call [MetadataOutput.start](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-startasynccallbackunit) to start outputting metadata. If the API call fails, an error code is returned. For details about the error code types, see [Camera Error Codes](../../reference/CameraKit/cj-errorcode-multimedia-camera.md).

    <!-- compile -->

    ```cangjie
    func startMetadataStream(metadataOutput: MetadataOutput): Unit {
        let callback: AsyncCallback<Unit> = {
            err: Option<BusinessException>, data: Option<Unit> =>
            if (let Some(e) <- err) {
                Hilog.error(0, "test", "Failed to metadataOutput start. error code: ${e.code}")
            } else {
                Hilog.info(0, "test", "Callback returned with metadataOutput started.")
            }
        }
        metadataOutput.start(callback)
    }
    ```

5. Call [MetadataOutput.stop](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-stopasynccallbackunit) to stop outputting metadata. If the API call fails, an error code is returned. For details about the error code types, see [Camera Error Codes](../../reference/CameraKit/cj-errorcode-multimedia-camera.md).

    <!-- compile -->

    ```cangjie
    func stopMetadataStream(metadataOutput: MetadataOutput): Unit {
        let callback: AsyncCallback<Unit> = {
            err: Option<BusinessException>, data: Option<Unit> =>
            if (let Some(e) <- err) {
                Hilog.error(0, "test", "Failed to metadataOutput stop. error code: ${e.code}")
            } else {
                Hilog.info(0, "test", "Callback returned with metadataOutput stopped.")
            }
        }
        metadataOutput.stop(callback)
    }
    ```

## Status Listening

During camera application development, you can listen for the status of metadata and the output stream at any time.

- Obtain the metadata object by registering a listener. Call [onMetadataObjectsAvailable](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-onmetadataobjectsavailablecallback1argumentarraymetadataobject) to subscribe to the callback. When valid metadata is detected, the callback returns the corresponding metadata information. The listening is available after metadataOutput is successfully created.

    <!-- compile -->

    ```cangjie
    import kit.CangjieKit.Callback1Argument

    class MetadataObjectsAvailableCallback <: Callback1Argument<Array<MetadataObject>> {
        public open func invoke(err: ?BusinessException, metadataObjectArr: Array<MetadataObject>): Unit {
            for (obj in metadataObjectArr) {
                Hilog.info(0, "test", "metadata output metadataObjectsAvailable, type: ${obj.metadataObjectType}")
            }
        }
    }

    func onMetadataObjectsAvailable(metadataOutput: MetadataOutput): Unit {
        metadataOutput.onMetadataObjectsAvailable(MetadataObjectsAvailableCallback())
    }
    ```

    > **Note:**
    >
    > Currently, only the face detection ([FaceDetection](../../reference/CameraKit/cj-apis-multimedia-camera.md#facedetection)) capability is supported for metadata types. The metadata information object is the rectangle information ([Rect](../../reference/CameraKit/cj-apis-multimedia-camera.md#class-rect)) of the recognized face area, including the x-coordinate and y-coordinate of the top-left corner of the rectangle area and the width and height of the rectangle.

- Obtain the error result of listening to the metadata stream by registering a callback. Call [onError](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-onerrorcallback0argument) to subscribe to the callback. The callback returns the error code returned when an error occurs during the use of the metadata output API. For details about the error code types, see [Camera Error Codes](../../reference/CameraKit/cj-errorcode-multimedia-camera.md).

    <!-- compile -->

    ```cangjie
    import kit.CangjieKit.Callback0Argument

    class MetadataErrorCallback <: Callback0Argument {
        public open func invoke(err: ?BusinessException): Unit {
            if (let Some(e) <- err) {
                Hilog.error(0, "test", "Metadata output error code: ${e.code}")
            }
        }
    }

    func onMetadataError(metadataOutput: MetadataOutput): Unit {
        metadataOutput.onError(MetadataErrorCallback())
    }
    ```
