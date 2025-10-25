# Camera Recovery Practice (Cangjie)

This example provides a comprehensive introduction to the camera application's recovery process when switching from background to foreground, helping developers understand the complete interface invocation sequence.

Explanation of camera application state changes during background/foreground switching:

- When the camera application moves to the background, it will be forcibly disconnected due to security policies. At this time, the camera status callback will return an available state, indicating that the camera device has been closed and is idle.
- When the camera application switches from background to foreground, the camera status callback will return an unavailable state, indicating that the camera device is currently opened and busy.
- When switching from background to foreground, the camera application needs to restart the camera device's preview stream, capture stream, and camera session management.

Before referring to this example, developers are advised to review specific sections of the [Camera Development Guide (Cangjie)](./cj-camera-preparation.md), including [Camera Management](./cj-camera-device-management.md), [Device Input](./cj-camera-device-input.md), and [Session Management](./cj-camera-session-management.md).

## Development Process

The recommended invocation flowchart for camera application recovery when switching from background to foreground:

![Camera Background recovery processing](./figures/camera-background-recovery.png)

## Complete Example

For context acquisition methods, please refer to: [Obtaining UIAbility Context Information](../../application-models/cj-uiability-usage.md#获取uiability的上下文信息).

Camera application recovery when switching from background to foreground needs to be called in the page lifecycle callback function onPageShow to reinitialize the camera device.

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
        // When the application switches from background to foreground page display, reinitialize the camera device.
        initCamera(context, surfaceId)
    }

    func initCamera(baseContext: UIAbilityContext, surfaceId: String): Unit {
        Hilog.info(0,"",'onForeGround recovery begin.')
        let cameraManager: CameraManager = getCameraManager(context)
        // Monitor camera status changes.
        cameraManager.on(CameraEvents.CameraStatus, Cb1())

        // Get camera list.
        let cameraArray: Array<CameraDevice> = cameraManager.getSupportedCameras()
        if (cameraArray.size <= 0) {
            Hilog.error(0,"","cameraManager.getSupportedCameras error")
            return
        }

        for (index in 0..cameraArray.size) {
            Hilog.info(0,"",'cameraId : ' + cameraArray[index].cameraId) // Get camera ID.
            Hilog.info(0,"",'cameraPosition : ' + cameraArray[index]
                .cameraPosition
                .toString()) // Get camera position.
            Hilog.info(0,"",'cameraType : ' + cameraArray[index]
                .cameraType
                .toString()) // Get camera type.
            Hilog.info(0,"",'connectionType : ' + cameraArray[index]
                .connectionType
                .toString()) // Get camera connection type.
        }

        // Create camera input stream.
        var cameraInput: ?CameraInput = None
        try {
            cameraInput = cameraManager.createCameraInput(cameraArray[0])
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to createCameraInput errorCode = ${err.code}')
        }
        if (cameraInput.isNone()) {
            return
        }

        // Monitor cameraInput error messages.
        let cameraDevice: CameraDevice = cameraArray[0]
        cameraInput?.on(CameraEvents.CameraError, cameraDevice, Cb2())

        // Open camera.
        cameraInput?.open()

        // Get supported mode types.
        let sceneModes: Array<SceneMode> = cameraManager.getSupportedSceneModes(cameraArray[0])
        let isSupportPhotoMode: Bool = sceneModes
            .indexOf(SceneMode.NormalPhoto)
            .getOrThrow() >= 0
        if (!isSupportPhotoMode) {
            Hilog.error(0,"",'photo mode not support')
            return
        }
        // Get camera device supported output capabilities.
        let cameraOutputCap: CameraOutputCapability = cameraManager.getSupportedOutputCapability(cameraArray[0],
            SceneMode.NormalPhoto)
        Hilog.info(0,"","outputCapability: ")

        let previewProfilesArray: Array<Profile> = cameraOutputCap.previewProfiles

        let photoProfilesArray: Array<Profile> = cameraOutputCap.photoProfiles

        // Create preview output stream, where the surfaceId parameter refers to the XComponent mentioned above, and the preview stream is the surface provided by the XComponent.
        var previewOutput: ?PreviewOutput = None
        try {
            previewOutput = cameraManager.createPreviewOutput(previewProfilesArray[0], surfaceId)
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to create the PreviewOutput instance. error code: ${err.code}')
        }
        if (previewOutput.isNone()) {
            return
        }
        // Monitor preview output error messages.
        previewOutput?.on(CameraEvents.CameraError, Cb3())

        // Create photo output stream.
        var photoOutput: ?PhotoOutput = None
        try {
            photoOutput = cameraManager.createPhotoOutput(profile:photoProfilesArray[0])
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to createPhotoOutput errorCode = ${err.code}')
        }
        if (photoOutput.isNone()) {
            return
        }

        // Create session.
        var photoSession: ?PhotoSession = None
        try {
            photoSession = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to create the session instance. errorCode = ${err.code}')
        }
        if (photoSession.isNone()) {
            return
        }
        // Monitor session error messages.
        photoSession?.on(CameraEvents.CameraError, Cb4())

        // Start configuring session.
        try {
            photoSession?.beginConfig()
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to beginConfig. errorCode = ')
        }

        // Add camera input stream to session.
        try {
            photoSession?.addInput(cameraInput.getOrThrow())
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to addInput. errorCode = ${err.code}')
        }

        // Add preview output stream to session.
        try {
            photoSession?.addOutput(previewOutput.getOrThrow())
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to addOutput(previewOutput). errorCode = ${err.code}')
        }

        // Add photo output stream to session.
        try {
            photoSession?.addOutput(photoOutput.getOrThrow())
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to addOutput(photoOutput). errorCode = ${err.code}')
        }

        // Commit session configuration.
        photoSession?.commitConfig()

        // Start session.
        photoSession?.start()
        // Check if device supports flash.
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
            // Check if auto flash mode is supported.
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
                // Set auto flash mode.
                try {
                    photoSession?.setFlashMode(FlashMode.FlashModeAuto)
                } catch (err: BusinessException) {
                    Hilog.error(0,"",'Failed to set the flash mode. errorCode = ${err.code}')
                }
            }
        }

        // Check if continuous auto focus mode is supported.
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
            // Set continuous auto focus mode.
            try {
                photoSession?.setFocusMode(FocusMode.FocusModeContinuousAuto)
            } catch (err: BusinessException) {
                Hilog.error(0,"",'Failed to set the focus mode. errorCode = ${err.code}')
            }
        }

        // Get supported zoom ratio range for camera.
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
        // Set zoom ratio.
        try {
            photoSession?.setZoomRatio(zoomRatioRange[0])
        } catch (err: BusinessException) {
            Hilog.error(0,"",'Failed to set the zoom ratio value. errorCode = ${err.code}')
        }
        let photoCaptureSetting: PhotoCaptureSetting = PhotoCaptureSetting(
            quality: QualityLevel.QualityLevelHigh, // Set high image quality.
            rotation: ImageRotation.Rotation0 // Set image rotation angle to 0.
        )
        // Capture photo with current settings.
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