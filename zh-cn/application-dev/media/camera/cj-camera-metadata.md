# 元数据

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

在开发相机应用时，需要先[申请相关权限](cj-camera-preparation.md)。

元数据（Metadata）是对相机返回的图像信息的描述和上下文。针对图像信息，提供更详细的数据，如照片或视频中，识别人像的取景框坐标的信息等。

Metadata主要是通过一个TAG（Key），去找对应的Data，用于传递参数和配置信息，减少内存拷贝操作。

## 适用场景

检测图片中的人脸，返回高精度的人脸矩形框坐标。应用可基于人脸定位结果，灵活集成后处理算法，将其应用于多样化场景。

## 开发步骤

详细的API说明请参见[Camera API参考](../../reference/CameraKit/cj-apis-multimedia-camera.md)。

1. 导入相关接口，导入方法如下。

    <!-- compile -->

    ```cangjie
    import kit.CameraKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. 调用[CameraOutputCapability](../../reference/CameraKit/cj-apis-multimedia-camera.md#class-cameraoutputcapability)中的[supportedMetadataObjectTypes](../../reference/CameraKit/cj-apis-multimedia-camera.md#let-supportedmetadataobjecttypes)属性，获取当前设备支持的元数据类型，并通过[createMetadataOutput](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-createmetadataoutputarraymetadataobjecttype)方法创建元数据输出流。

    <!-- compile -->

    ```cangjie
    func getMetadataOutput(cameraManager: CameraManager, cameraOutputCapability: CameraOutputCapability): MetadataOutput {
        let metadataObjectTypes: Array<MetadataObjectType> = cameraOutputCapability.supportedMetadataObjectTypes
        let metadataOutput = cameraManager.createMetadataOutput(metadataObjectTypes)
        return metadataOutput
    }
    ```

3. 会话配置。向会话中添加相机的输入流和元数据输出流，调用[commitConfig](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-commitconfig)和[start](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-start)方法提交相关配置，并启动会话。

    设备输入（cameraInput）与预览输出（previewOutput）的获取方式请参考[设备输入](cj-camera-device-input.md#开发步骤)和[相机预览开发步骤](cj-camera-device-input.md)。

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

4. 调用[MetadataOutput.start](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-startasynccallbackunit)方法开始输出元数据，接口调用失败时，会返回相应错误码，错误码类型参见[Camera错误码](../../reference/CameraKit/cj-errorcode-multimedia-camera.md)。

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

5. 调用[MetadataOutput.stop](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-stopasynccallbackunit)方法停止输出元数据，接口调用失败会返回相应错误码，错误码类型参见[Camera错误码](../../reference/CameraKit/cj-errorcode-multimedia-camera.md)。

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

## 状态监听

在相机应用开发过程中，可以随时监听metadata数据以及输出流的状态。

- 通过注册监听获取metadata对象，调用[onMetadataObjectsAvailable](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-onmetadataobjectsavailablecallback1argumentarraymetadataobject)接口订阅回调。检测到有效metadata数据时，callback返回相应的metadata数据信息，metadataOutput创建成功时可监听。

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

    > **说明：**
    >
    > 当前的元数据类型仅支持人脸检测（[FaceDetection](../../reference/CameraKit/cj-apis-multimedia-camera.md#facedetection)）功能。元数据信息对象为识别到的人脸区域的矩形信息（[Rect](../../reference/CameraKit/cj-apis-multimedia-camera.md#class-rect)），包含矩形区域的左上角x坐标、y坐标和矩形的宽高数据。

- 通过注册回调函数，获取监听metadata流的错误结果，调用[onError](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-onerrorcallback0argument)接口订阅回调，callback返回metadata输出接口使用错误时返回的错误码，错误码类型参见[Camera错误码](../../reference/CameraKit/cj-errorcode-multimedia-camera.md)。

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
