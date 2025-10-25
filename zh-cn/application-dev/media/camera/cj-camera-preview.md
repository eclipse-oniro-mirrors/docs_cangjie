# 预览（仓颉）

在开发相机应用时，需要先参考开发准备[申请相关权限](./cj-camera-preparation.md)。

预览是启动相机后看见的画面，通常在拍照和录像前执行。

## 开发步骤

详细的API说明请参见[Camera API参考](../../../../zh-cn/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md)。

1. 导入camera接口，接口中提供了相机相关的属性和方法，导入方法如下。

    <!-- compile -->

    ```cangjie
    import kit.CameraKit.*
    import ohos.hilog.Hilog
    import ohos.callback_invoke.Callback0Argument
    import ohos.business_exception.BusinessException
    ```

2. 创建Surface。

    XComponent组件为预览流提供的Surface，而XComponent的能力由UI提供。

    > **说明：**
    >
    > 预览流与录像输出流的分辨率的宽高比要保持一致，如果设置XComponent组件中的Surface显示区域宽高比为1920:1080 = 16:9，则需要预览流中的分辨率的宽高比也为16:9，如分辨率选择640:360，或960:540，或1920:1080，以此类推。

3. 通过[CameraOutputCapability](../../../../zh-cn/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#struct-cameraoutputcapability)类中的previewProfiles属性获取当前设备支持的预览能力，返回previewProfilesArray数组 。通过[createPreviewOutput](../../../../zh-cn/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-createpreviewoutputprofile-string)方法创建预览输出流，其中，[createPreviewOutput](../../../../zh-cn/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-createpreviewoutputprofile-string)方法中的两个参数分别是previewProfilesArray数组中的第一项和步骤二中获取的surfaceId。

    <!-- compile -->

    ```cangjie
    func getPreviewOutput(cameraManager: CameraManager, cameraOutputCapability: CameraOutputCapability, surfaceId: String): PreviewOutput {
        let previewProfilesArray: Array<Profile> = cameraOutputCapability.previewProfiles
        let previewOutput: PreviewOutput = cameraManager.createPreviewOutput(previewProfilesArray[0], surfaceId)
        return previewOutput
    }
    ```

4. 使能。通过[Session.start](../../../../zh-cn/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-start)方法输出预览流，接口调用失败会返回相应错误码，错误码类型参见[Camera错误码](../../../../zh-cn/application-dev/reference/CameraKit/cj-errorcode-multimedia-camera.md)。

    <!-- compile -->

    ```cangjie
    func startPreviewOutput(cameraManager: CameraManager, previewOutput: PreviewOutput): Unit {
        let cameraArray: Array<CameraDevice> = cameraManager.getSupportedCameras()
        if (cameraArray.size == 0) {
            Hilog.error(0,"",'no camera.')
            return
        }
        // 获取支持的模式类型。
        let sceneModes: Array<SceneMode> = cameraManager.getSupportedSceneModes(cameraArray[0])
        let isSupportPhotoMode: Bool = sceneModes.indexOf(SceneMode.NormalPhoto).isSome()
        if (!isSupportPhotoMode) {
            Hilog.error(0,"",'photo mode not support')
            return
        }
        let cameraInput: CameraInput = cameraManager.createCameraInput(cameraArray[0])
        // 打开相机。
        cameraInput.open()
        let session: PhotoSession = (cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession).getOrThrow()
        session.beginConfig()
        session.addInput(cameraInput)
        session.addOutput(previewOutput)
        session.commitConfig()
        session.start()
    }
    ```

## 状态监听

在相机应用开发过程中，可以随时监听预览输出流状态，包括预览流启动、预览流结束、预览流输出错误。

- 通过注册固定的frameStart回调函数获取监听预览启动结果，previewOutput创建成功时即可监听，预览第一次曝光时触发，有该事件返回结果则认为预览流已启动。

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

- 通过注册固定的frameEnd回调函数获取监听预览结束结果，previewOutput创建成功时即可监听，预览完成最后一帧时触发，有该事件返回结果则认为预览流已结束。

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

- 通过注册固定的error回调函数获取监听预览输出错误结果，回调返回预览输出接口使用错误时对应的错误码，错误码类型参见[Camera错误码](../../../../zh-cn/application-dev/reference/CameraKit/cj-errorcode-multimedia-camera.md)。

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
