# 相机启动恢复实践(仓颉)

当前示例提供完整的相机应用从后台切换至前台启动恢复的流程介绍，方便开发者了解完整的接口调用顺序。

相机应用在前后台切换过程中的状态变化说明：

- 当相机应用在退后台之后由于安全策略会被强制断流，并且此时相机状态回调会返回相机可用状态，表示当前相机设备已经被关闭，处于空闲状态。
- 当相机应用从后台切换至前台时，相机状态回调会返回相机不可用状态，表示当前相机设备被打开，处于忙碌状态。
- 相机应用从后台切换至前台时，需要重启相机设备的预览流、拍照流以及相机会话管理。

在参考以下示例前，建议开发者查看[相机开发指导(仓颉)](./cj-camera-preparation.md)的具体章节，了解[相机管理](./cj-camera-device-management.md)、[设备输入](./cj-camera-device-input.md)、[会话管理](./cj-camera-session-management.md)等单个操作。

## 开发流程

相机应用从后台切换至前台启动恢复调用流程图建议如下：

![Camera Background recovery processing](./figures/camera-background-recovery.png)

## 完整示例

Context获取方式请参见：[获取UIAbility的上下文信息](../../application-models/cj-uiability-usage.md#获取uiability的上下文信息)。

相机应用从后台切换至前台启动恢复需要在页面生命周期回调函数onPageShow中调用，重新初始化相机设备。

<!-- compile -->

```cangjie
package ohos_app_cangjie_entry
internal import ohos.base.LengthProp
internal import ohos.arkui.component.Column
internal import ohos.arkui.component.Row
internal import ohos.arkui.component.Text
internal import ohos.arkui.component.CustomView
internal import ohos.arkui.component.CJEntry
internal import ohos.arkui.component.loadNativeView
internal import ohos.arkui.component.FontWeight
internal import ohos.arkui.state_management.SubscriberManager
internal import ohos.arkui.state_management.ObservedProperty
internal import ohos.arkui.state_management.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import ohos.arkui.state_macro_manage.State
import ohos.arkui.state_macro_manage.r
import kit.AbilityKit.*
import kit.CameraKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*
import ohos.hilog.Hilog
import ohos.multimedia.camera

var ctx = None<UIAbilityContext>

@Entry
@Component
class EntryView {
    @State
    var message: String = "Hello World"

    let context = ctx.getOrThrow()
    let surfaceId: String = ''
    protected override func onPageShow() {
        // 当应用从后台切换至前台页面显示时，重新初始化相机设备。
        initCamera(context, surfaceId)
    }

    func initCamera(baseContext: UIAbilityContext, surfaceId: String): Unit {
        Hilog.info(0,"",'onForeGround recovery begin.')
        let cameraManager: CameraManager = getCameraManager(context)
        // 监听相机状态变化。
        cameraManager.on(CameraEvents.CameraStatus, Cb1())

        // 获取相机列表。
        let cameraArray: Array<CameraDevice> = cameraManager.getSupportedCameras()
        if (cameraArray.size <= 0) {
            Hilog.error(0,"","cameraManager.getSupportedCameras error")
            return
        }

        for (index in 0..cameraArray.size) {
            Hilog.info(0,"",'cameraId : ' + cameraArray[index].cameraId) // 获取相机ID。
            Hilog.info(0,"",'cameraPosition : ' + cameraArray[index]
                .cameraPosition
                .toString()) // 获取相机位置。
            Hilog.info(0,"",'cameraType : ' + cameraArray[index]
                .cameraType
                .toString()) // 获取相机类型。
            Hilog.info(0,"",'connectionType : ' + cameraArray[index]
                .connectionType
                .toString()) // 获取相机连接类型。
        }

        // 创建相机输入流。
        var cameraInput: ?CameraInput = None
        try {
            cameraInput = cameraManager.createCameraInput(cameraArray[0])
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to createCameraInput errorCode = ${err.code}')
        }
        if (cameraInput.isNone()) {
            return
        }

        // 监听cameraInput错误信息。
        let cameraDevice: CameraDevice = cameraArray[0]
        cameraInput?.on(CameraEvents.CameraError, cameraDevice, Cb2())

        // 打开相机。
        cameraInput?.open()

        // 获取支持的模式类型。
        let sceneModes: Array<SceneMode> = cameraManager.getSupportedSceneModes(cameraArray[0])
        let isSupportPhotoMode: Bool = sceneModes
            .indexOf(SceneMode.NormalPhoto)
            .getOrThrow() >= 0
        if (!isSupportPhotoMode) {
            Hilog.error(0,"",'photo mode not support')
            return
        }
        // 获取相机设备支持的输出流能力。
        let cameraOutputCap: CameraOutputCapability = cameraManager.getSupportedOutputCapability(cameraArray[0],
            SceneMode.NormalPhoto)
        Hilog.info(0,"","outputCapability: ")

        let previewProfilesArray: Array<Profile> = cameraOutputCap.previewProfiles

        let photoProfilesArray: Array<Profile> = cameraOutputCap.photoProfiles

        // 创建预览输出流,其中参数 surfaceId 参考上文 XComponent 组件，预览流为XComponent组件提供的surface。
        var previewOutput: ?PreviewOutput = None
        try {
            previewOutput = cameraManager.createPreviewOutput(previewProfilesArray[0], surfaceId)
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to create the PreviewOutput instance. error code: ${err.code}')
        }
        if (previewOutput.isNone()) {
            return
        }
        // 监听预览输出错误信息。
        previewOutput?.on(CameraEvents.CameraError, Cb3())

        // 创建拍照输出流。
        var photoOutput: ?PhotoOutput = None
        try {
            photoOutput = cameraManager.createPhotoOutput(profile:photoProfilesArray[0])
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to createPhotoOutput errorCode = ${err.code}')
        }
        if (photoOutput.isNone()) {
            return
        }

        //创建会话。
        var photoSession: ?PhotoSession = None
        try {
            photoSession = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to create the session instance. errorCode = ${err.code}')
        }
        if (photoSession.isNone()) {
            return
        }
        // 监听session错误信息。
        photoSession?.on(CameraEvents.CameraError, Cb4())

        // 开始配置会话。
        try {
            photoSession?.beginConfig()
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to beginConfig. errorCode = ')
        }

        // 向会话中添加相机输入流。
        try {
            photoSession?.addInput(cameraInput.getOrThrow())
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to addInput. errorCode = ${err.code}')
        }

        // 向会话中添加预览输出流。
        try {
            photoSession?.addOutput(previewOutput.getOrThrow())
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to addOutput(previewOutput). errorCode = ${err.code}')
        }

        // 向会话中添加拍照输出流。
        try {
            photoSession?.addOutput(photoOutput.getOrThrow())
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to addOutput(photoOutput). errorCode = ${err.code}')
        }

        // 提交会话配置。
        photoSession?.commitConfig()

        // 启动会话。
        photoSession?.start()
        // 判断设备是否支持闪光灯。
        var flashStatus: Bool = false
        try {
            flashStatus = photoSession
                .getOrThrow()
                .hasFlash()
        } catch (err: BusinessException) {
           Hilog.error(0,"",'Failed to hasFlash. errorCode = ${err.code}')
        }
        Hilog.info(0,"",'Returned with the flash light support status: ${flashStatus}')

        if (flashStatus) {
            // 判断是否支持自动闪光灯模式。
            var flashModeStatus: Bool = false
            try {
                let status: Bool = photoSession
                    .getOrThrow()
                    .isFlashModeSupported(FlashMode.FlashModeAuto)
                flashModeStatus = status
            } catch (err: BusinessException) {
                Hilog.error(0,"",'Failed to check whether the flash mode is supported. errorCode = ${err.code}')
            }
            if (flashModeStatus) {
                // 设置自动闪光灯模式。
                try {
                    photoSession?.setFlashMode(FlashMode.FlashModeAuto)
                } catch (err: BusinessException) {
                    Hilog.error(0,"",'Failed to set the flash mode. errorCode = ${err.code}')
                }
            }
        }

        // 判断是否支持连续自动变焦模式。
        var focusModeStatus: Bool = false
        try {
            let status: Bool = photoSession
                .getOrThrow()
                .isFocusModeSupported(FocusMode.FocusModeContinuousAuto)
            focusModeStatus = status
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to check whether the focus mode is supported. errorCode = ${err.code}')
        }

        if (focusModeStatus) {
            // 设置连续自动变焦模式。
            try {
                photoSession?.setFocusMode(FocusMode.FocusModeContinuousAuto)
            } catch (err: BusinessException) {
                Hilog.error(0,"",'Failed to set the focus mode. errorCode = ${err.code}')
            }
        }

        // 获取相机支持的可变焦距比范围。
        var zoomRatioRange: Array<Float64> = []
        try {
            zoomRatioRange = photoSession
                .getOrThrow()
                .getZoomRatioRange()
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to get the zoom ratio range. errorCode = ${err.code}')
        }
        if (zoomRatioRange.size <= 0) {
            return
        }
        // 设置可变焦距比。
        try {
            photoSession?.setZoomRatio(zoomRatioRange[0])
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to set the zoom ratio value. errorCode = ${err.code}')
        }
        let photoCaptureSetting: PhotoCaptureSetting = PhotoCaptureSetting(
            quality: QualityLevel.QualityLevelHigh, // 设置图片质量高。
            rotation: ImageRotation.Rotation0 // 设置图片旋转角度0。
        )
        // 使用当前拍照设置进行拍照。
        photoOutput?.capture(photoCaptureSetting)

        Hilog.info(0,"",'onForeGround recovery end.')
    }

    func build() {
        Row {
            Column {
                Text(this.message)
                    .fontSize(50)
                    .fontWeight(FontWeight.Bold)
                    .onClick {
                        evt =>
                    }
            }.width(100.percent)
        }.height(100.percent)
    }
}

class Cb1 <: Callback1Argument<CameraStatusInfo> {
    public func invoke(error: ?BusinessException,cameraStatusInfo: CameraStatusInfo): Unit {
        Hilog.info(0,"",'camera : ${cameraStatusInfo.camera.cameraId}')
        Hilog.info(0,"",'status: ${cameraStatusInfo.status}')
    }
}

class Cb2 <: Callback0Argument {
    public func invoke(error: ?BusinessException): Unit {
        if (let Some(e) <- error) {
            Hilog.error(0,"",'Camera input error code: ${e.code}',"")
        }

    }
}

class Cb3 <: Callback0Argument {
    public func invoke(error: ?BusinessException): Unit {
        if (let Some(e) <- error) {
            Hilog.error(0,"",'Camera input error code: ${e.code}',"")
        }
    }
}

class Cb4 <: Callback0Argument {
    public func invoke(error: ?BusinessException): Unit {
      if (let Some(e) <- error) {
            Hilog.error(0,"",'Camera input error code: ${e.code}',"")
        }
    }
}

```
