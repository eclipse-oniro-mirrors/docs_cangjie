# ohos.multimedia.camera (Camera Management)

This module provides developers with a set of simple and easy-to-understand camera service interfaces, enabling them to develop camera applications. Through accessing and operating camera hardware, applications can perform basic operations such as preview, photo capture, and video recording. Additionally, more advanced operations can be achieved by combining interfaces, such as controlling flashlights, exposure time, focus or zoom adjustments.

## Importing the Module

```cangjie
import kit.CameraKit.*
```

## Permission List

ohos.permission.CAMERA

ohos.permission.MICROPHONE

## Usage Instructions

API sample code usage instructions:

- If the sample code's first line contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## func getCameraManager(UIAbilityContext)

```cangjie
public func getCameraManager(context: UIAbilityContext): CameraManager
```

**Function:** Obtains a camera manager instance.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [CameraManager](#class-cameramanager) | Camera manager. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions above.
    let cameraManager = getCameraManager(ctx)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface AutoExposure

```cangjie
public interface AutoExposure <: AutoExposureQuery {
    func getExposureMode(): ExposureMode
    func setExposureMode(aeMode: ExposureMode): Unit
    func getMeteringPoint(): Point
    func setMeteringPoint(point: Point): Unit
    func setExposureBias(exposureBias: Float64): Unit
    func getExposureValue(): Float64
}
```

**Function:** Device auto-exposure (AE) operations.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parent Type:**

- [AutoExposureQuery](#interface-autoexposurequery)

### func getExposureMode()

```cangjie
func getExposureMode(): ExposureMode
```

**Function:** Obtains the current exposure mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [ExposureMode](#enum-exposuremode) | Current exposure mode. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions above.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    let photoSession = session as PhotoSession
    Hilog.info(0, "AppLogCj", photoSession.getOrThrow().getExposureMode().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getExposureValue()

```cangjie
func getExposureValue(): Float64
```

**Function:** Queries the current exposure value.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Float64 | Exposure value. Exposure compensation has a step size. For example, if the step size is 0.5, setting 1.2 will result in an actual effective exposure compensation of 1.0. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions above.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    let photoSession = session as PhotoSession
    Hilog.info(0, "AppLogCj", photoSession.getOrThrow().getExposureValue().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getMeteringPoint()

```cangjie
func getMeteringPoint(): Point
```

**Function:** Queries the center point of the exposure area.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Point](#class-point) | Current exposure point. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions above.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    let photoSession = session as PhotoSession
    let point = photoSession.getOrThrow().getMeteringPoint()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setExposureBias(Float64)

```cangjie
func setExposureBias(exposureBias: Float64): Unit
```

**Function:** Sets exposure compensation (EV value).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| exposureBias | Float64 | Yes | - | Exposure compensation. Use [getExposureBiasRange](#func-getexposurebiasrange) to query the supported range. If the set value exceeds the supported range, it will automatically adjust to the nearest boundary. Exposure compensation has a step size. For example, if the step size is 0.5, setting 1.2 will result in an actual effective exposure compensation of 1.0. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400102 | Operation not allowed. |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions above.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let exposureBias = 1.2
    photoSession.setExposureBias(exposureBias)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setExposureMode(ExposureMode)

```cangjie
func setExposureMode(aeMode: ExposureMode): Unit
```

**Function:** Sets the exposure mode. Before setting, check whether the device supports the specified exposure mode using [isExposureModeSupported](#func-isexposuremodesupportedexposuremode).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| aeMode | [ExposureMode](#enum-exposuremode) | Yes | - | Exposure mode. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400102 | Operation not allowed. |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions above.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let aeMode = ExposureMode.ExposureModeAuto
    photoSession.setExposureMode(aeMode)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setMeteringPoint(Point)

```cangjie
func setMeteringPoint(point: Point): Unit
```

**Function:** Queries the center point of the exposure area.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| point | [Point](#class-point) | Yes | - | Current exposure point. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.CameraKit.Point as ImagePoint
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions above.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let point = ImagePoint(1.0, 1.0)
    photoSession.setMeteringPoint(point)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface AutoExposureQuery

```cangjie
public interface AutoExposureQuery {
    func isExposureModeSupported(aeMode: ExposureMode): Bool
    func getExposureBiasRange(): Array<Float64>
}
```

**Function:** Provides device auto-exposure feature query functionality.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

### func getExposureBiasRange()

```cangjie
func getExposureBiasRange(): Array<Float64>
```

**Function:** Queries the exposure compensation range.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Float64> | Array of compensation range. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions above.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let range = photoSession.getExposureBiasRange()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isExposureModeSupported(ExposureMode)

```cangjie
func isExposureModeSupported(aeMode: ExposureMode): Bool
```

**Function:** Checks whether the exposure mode is supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| aeMode | [ExposureMode](#enum-exposuremode) | Yes | - | Exposure mode. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether the exposure mode is supported. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config, only throw in session usage. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions above.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let aeMode = ExposureMode.ExposureModeAuto
    Hilog.info(0, "AppLogCj", photoSession.isExposureModeSupported(aeMode).toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## interface CameraOutput

```cangjie
public interface CameraOutput {
    func release(): Unit
}
```

**Description:** Base class for output information used by Session in a session.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func release()

```cangjie
func release(): Unit
```

**Description:** Releases output resources.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let previewOutput = cameraManager.createPreviewOutput(ability.previewProfiles[0], surfaceId)
    previewOutput.release()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface ColorManagement

```cangjie
public interface ColorManagement <: ColorManagementQuery {
    func setColorSpace(colorSpace: ColorSpace): Unit
    func getActiveColorSpace(): ColorSpace
}
```

**Description:** Manages color space parameters.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Type:**

- [ColorManagementQuery](#interface-colormanagementquery)

### func getActiveColorSpace()

```cangjie
func getActiveColorSpace(): ColorSpace
```

**Description:** Gets the currently set color space.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
|[ColorSpace](../ArkGraphics2D/cj-apis-color_manager.md#enum-colorspace)| Currently set color space. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let colorSpace = photoSession.getActiveColorSpace()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setColorSpace(ColorSpace)

```cangjie
func setColorSpace(colorSpace: ColorSpace): Unit
```

**Description:** Sets the color space. You can first obtain the supported ColorSpaces of the current device through [getSupportedColorSpaces](#func-getsupportedcolorspaces).

Applications can set different color space ([ColorSpace](../ArkGraphics2D/cj-apis-color_manager.md#enum-colorspace)) parameters to support P3 wide color gamut and HDR high dynamic range imaging.

When the application does not actively set the color space, the default for photo and video modes is HDR shooting effect.

Setting HDR high-display effect in photo mode directly supports P3 color gamut.

Applications can refer to the following table for enabling HDR effects and setting color spaces in different modes.

Table 1: Video Mode

| SDR/HRD Shooting | CameraFormat | ColorSpace |
|:---|:---|:---|
| SDR | CAMERA_FORMAT_YUV_420_SP | BT709_LIMIT |
| HDR_VIVID(Default) | CAMERA_FORMAT_YCRCB_P010 | BT2020_HLG_LIMIT |

Table 2: Photo Mode

| SDR/HRD Shooting | ColorSpace |
|:---|:---|
| SDR | Srgb |
| HDR_VIVID(Default) | DisplayP3 |

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| colorSpace | [ColorSpace](../ArkGraphics2D/cj-apis-color_manager.md#enum-colorspace) | Yes | - | Color space, obtained through the [getSupportedColorSpaces](#func-getsupportedcolorspaces) interface. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400102 | The colorSpace does not match the format. |
  | 7400103 | Session not config. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let colorSpace = photoSession.getSupportedColorSpaces()[0]
    photoSession.setColorSpace(colorSpace)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface ColorManagementQuery

```cangjie
public interface ColorManagementQuery {
    func getSupportedColorSpaces(): Array<ColorSpace>
}
```

**Description:** Queries color space parameters.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func getSupportedColorSpaces()

```cangjie
func getSupportedColorSpaces(): Array<ColorSpace>
```

**Description:** Gets the list of supported color spaces.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[ColorSpace](../ArkGraphics2D/cj-apis-color_manager.md#enum-colorspace)> | List of supported color spaces. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config, only throw in session usage. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let colorSpaces = photoSession.getSupportedColorSpaces()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface Flash

```cangjie
public interface Flash <: FlashQuery {
    func setFlashMode(flashMode: FlashMode): Unit
    func getFlashMode(): FlashMode
}
```

**Description:** Operates the device flash.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Type:**

- [FlashQuery](#interface-flashquery)

### func getFlashMode()

```cangjie
func getFlashMode(): FlashMode
```

**Description:** Gets the current flash mode of the device.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [FlashMode](#enum-flashmode) | Current flash mode of the device. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let flashMode = photoSession.getFlashMode()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setFlashMode(FlashMode)

```cangjie
func setFlashMode(flashMode: FlashMode): Unit
```

**Description:** Sets the flash mode.

Before setting, you need to check:

1. Whether the device supports flash, which can be determined using the [hasFlash](#func-hasflash) method.
2. Whether the device supports the specified flash mode, which can be determined using the [isFlashModeSupported](#func-isflashmodesupportedflashmode) method.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| flashMode | [FlashMode](#enum-flashmode) | Yes | - | Specified flash mode. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let flashMode = FlashMode.FlashModeAlwaysOpen
    photoSession.setFlashMode(flashMode)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface FlashQuery

```cangjie
public interface FlashQuery {
    func hasFlash(): Bool
    func isFlashModeSupported(flashMode: FlashMode): Bool
}
```

**Description:** Provides the ability to query the device's flash status and modes.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func hasFlash()

```cangjie
func hasFlash(): Bool
```

**Description:** Checks whether the device has a flash.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the device supports flash, false otherwise. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    Hilog.info(0, "AppLogCj", photoSession.hasFlash().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isFlashModeSupported(FlashMode)

```cangjie
func isFlashModeSupported(flashMode: FlashMode): Bool
```

**Description:** Checks whether the specified flash mode is supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| flashMode | [FlashMode](#enum-flashmode) | Yes | - | Specified flash mode. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the specified flash mode is supported, false otherwise. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    photoSession.isFlashModeSupported(FlashMode.FlashModeAlwaysOpen)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## interface Focus

```cangjie
public interface Focus <: FocusQuery {
    func setFocusMode(afMode: FocusMode): Unit
    func getFocusMode(): FocusMode
    func setFocusPoint(point: Point): Unit
    func getFocusPoint(): Point
    func getFocalLength(): Float64
}
```

**Functionality:** Device focus operations.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Type:**

- [FocusQuery](#interface-focusquery)

### func getFocalLength()

```cangjie
func getFocalLength(): Float64
```

**Functionality:** Queries the focal length value.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type    | Description |
|:--------|:------------|
| Float64 | Returns the current focal length in millimeters (mm). |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 7400103      | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    Hilog.info(0, "AppLogCj", photoSession.getFocalLength().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getFocusMode()

```cangjie
func getFocusMode(): FocusMode
```

**Functionality:** Gets the current focus mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type                     | Description |
|:-------------------------|:------------|
| [FocusMode](#enum-focusmode) | Current focus mode of the device. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 7400103      | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    Hilog.info(0, "AppLogCj", photoSession.getFocusMode().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getFocusPoint()

```cangjie
func getFocusPoint(): Point
```

**Functionality:** Queries the focus point.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type           | Description |
|:---------------|:------------|
| [Point](#class-point) | Current focus point. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 7400103      | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let point = photoSession.getFocusPoint()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setFocusMode(FocusMode)

```cangjie
func setFocusMode(afMode: FocusMode): Unit
```

**Functionality:** Sets the focus mode.

Before setting, check if the device supports the specified focus mode using [isFocusModeSupported](#func-isfocusmodesupportedfocusmode).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type                     | Required | Default | Description |
|:----------|:-------------------------|:---------|:--------|:------------|
| afMode    | [FocusMode](#enum-focusmode) | Yes      | -       | Specified focus mode. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 7400103      | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let afMode = FocusMode.FocusModeManual
    photoSession.setFocusMode(afMode)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setFocusPoint(Point)

```cangjie
func setFocusPoint(point: Point): Unit
```

**Functionality:** Sets the focus point within the 0-1 coordinate system, where the top-left corner is {0.0, 0.0} and the bottom-right corner is {1.0, 1.0}.

This coordinate system is based on the horizontal device orientation with the charging port on the right. For example, if the application's preview layout is based on the vertical orientation with the charging port at the bottom, and the layout dimensions are {w, h} with a touch point at {x, y}, the converted coordinate point is {y/h, 1-x/w}.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type           | Required | Default | Description |
|:----------|:---------------|:---------|:--------|:------------|
| point     | [Point](#class-point) | Yes      | -       | Focus point. x and y must be within [0.0, 1.0]. Values outside this range will be clamped to 0.0 if less than 0.0 or 1.0 if greater than 1.0. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 7400103      | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.CameraKit.Point as ImagePoint
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    photoSession.setFocusPoint(ImagePoint(0.5, 0.5))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface FocusQuery

```cangjie
public interface FocusQuery {
    func isFocusModeSupported(afMode: FocusMode): Bool
}
```

**Functionality:** Provides methods to check if a specified focus mode is supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func isFocusModeSupported(FocusMode)

```cangjie
func isFocusModeSupported(afMode: FocusMode): Bool
```

**Functionality:** Checks if a focus mode is supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type                     | Required | Default | Description |
|:----------|:-------------------------|:---------|:--------|:------------|
| afMode    | [FocusMode](#enum-focusmode) | Yes      | -       | Specified focus mode. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| Bool | Returns true if the focus mode is supported, false otherwise. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 7400103      | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let afMode = FocusMode.FocusModeManual
    Hilog.info(0, "AppLogCj", photoSession.isFocusModeSupported(afMode).toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface Session

```cangjie
public interface Session {
    func beginConfig(): Unit
    func commitConfig(): Unit
    func canAddInput(cameraInput: CameraInput): Bool
    func addInput(cameraInput: CameraInput): Unit
    func removeInput(cameraInput: CameraInput): Unit
    func canAddOutput(cameraOutput: CameraOutput): Bool
    func addOutput(cameraOutput: CameraOutput): Unit
    func removeOutput(cameraOutput: CameraOutput): Unit
    func start(): Unit
    func stop(): Unit
    func release(): Unit
}
```

**Functionality:** Session type that holds all resources required for a camera operation ([CameraInput](#class-camerainput), [CameraOutput](#interface-cameraoutput)) and requests camera functions (recording, photo capture) from the camera device.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func addInput(CameraInput)

```cangjie
func addInput(cameraInput: CameraInput): Unit
```

**Functionality:** Adds a [CameraInput](#class-camerainput) to the session.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter   | Type                     | Required | Default | Description |
|:------------|:-------------------------|:---------|:--------|:------------|
| cameraInput | [CameraInput](#class-camerainput) | Yes      | -       | CameraInput instance to be added. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 7400101      | Parameter missing or parameter type incorrect. |
  | 7400102      | Operation not allowed. |
  | 7400201      | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let cameraInput = cameraManager.createCameraInput(cameraDevice)
    session.addInput(cameraInput)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func addOutput(CameraOutput)

```cangjie
func addOutput(cameraOutput: CameraOutput): Unit
```

**Function:** Adds a [CameraOutput](#interface-cameraoutput) to the session.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| cameraOutput | [CameraOutput](#interface-cameraoutput) | Yes | - | The CameraOutput instance to be added. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400102 | Operation not allowed. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(cameraDevice)[0]
    let ability = cameraManager.getSupportedOutputCapability(cameraDevice, mode)
    let cameraOutput = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    session.addOutput(cameraOutput)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func beginConfig()

```cangjie
func beginConfig(): Unit
```

**Function:** Starts session configuration.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400105 | Session config locked. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    session.beginConfig()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func canAddInput(CameraInput)

```cangjie
func canAddInput(cameraInput: CameraInput): Bool
```

**Function:** Checks whether the current cameraInput can be added to the session.

This method takes effect only when called between [beginConfig](#func-beginconfig) and [commitConfig](#func-commitconfig).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| cameraInput | [CameraInput](#class-camerainput) | Yes | - | The CameraInput instance to be added. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the current cameraInput can be added; otherwise, returns false. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let cameraInput = cameraManager.createCameraInput(cameraDevice)
    Hilog.info(0, "AppLogCj", session.canAddInput(cameraInput).toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func canAddOutput(CameraOutput)

```cangjie
func canAddOutput(cameraOutput: CameraOutput): Bool
```

**Function:** Checks whether the current cameraOutput can be added to the session.

This method takes effect only when called between [beginConfig](#func-beginconfig) and [commitConfig](#func-commitconfig).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| cameraOutput | [CameraOutput](#interface-cameraoutput) | Yes | - | The CameraOutput instance to be added. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether the current cameraOutput can be added to the session. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(cameraDevice)[0]
    let ability = cameraManager.getSupportedOutputCapability(cameraDevice, mode)
    let cameraOutput = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    Hilog.info(0, "AppLogCj", session.canAddOutput(cameraOutput).toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func commitConfig()

```cangjie
func commitConfig(): Unit
```

**Function:** Commits the configuration.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400102 | Operation not allowed. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    session.commitConfig()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func release()

```cangjie
func release(): Unit
```

**Function:** Releases session resources.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    session.release()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func removeInput(CameraInput)

```cangjie
func removeInput(cameraInput: CameraInput): Unit
```

**Function:** Removes the specified CameraInput from the session.

This method takes effect only when called between [beginConfig](#func-beginconfig) and [commitConfig](#func-commitconfig).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| cameraInput | [CameraInput](#class-camerainput) | Yes | - | The CameraInput instance to be removed. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400102 | Operation not allowed. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let cameraInput = cameraManager.createCameraInput(cameraDevice)
    session.removeInput(cameraInput)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func removeOutput(CameraOutput)

```cangjie
func removeOutput(cameraOutput: CameraOutput): Unit
```

**Function:** Removes the specified CameraOutput from the session.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| cameraOutput | [CameraOutput](#interface-cameraoutput) | Yes | - | The CameraOutput instance to be removed. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400102 | Operation not allowed. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(cameraDevice)[0]
    let ability = cameraManager.getSupportedOutputCapability(cameraDevice, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let previewOutput = cameraManager.createPreviewOutput(ability.previewProfiles[0], surfaceId)
    session.removeOutput(previewOutput)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func start()

```cangjie
func start(): Unit
```

**Function:** Starts the session.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400102 | Operation not allowed. |
  | 7400103 | Session not config. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    session.start()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func stop()

```cangjie
func stop(): Unit
```

**Function:** Stops the session.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    session.stop()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## interface Stabilization

```cangjie
public interface Stabilization <: StabilizationQuery {
    func getActiveVideoStabilizationMode(): VideoStabilizationMode
    func setVideoStabilizationMode(mode: VideoStabilizationMode): Unit
}
```

**Function:** Provides operations related to video stabilization during recording mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Type:**

- [StabilizationQuery](#interface-stabilizationquery)

### func getActiveVideoStabilizationMode()

```cangjie
func getActiveVideoStabilizationMode(): VideoStabilizationMode
```

**Function:** Queries the currently active video stabilization mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[VideoStabilizationMode](#enum-videostabilizationmode)|Whether video stabilization is currently active.|

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required, see usage instructions
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalVideo)
    var videoSessionOption = session as VideoSession
    let videoSession = videoSessionOption.getOrThrow()
    Hilog.info(0, "AppLogCj", videoSession.getActiveVideoStabilizationMode().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setVideoStabilizationMode(VideoStabilizationMode)

```cangjie
func setVideoStabilizationMode(mode: VideoStabilizationMode): Unit
```

**Function:** Sets the video stabilization mode. First check whether the device supports the specified stabilization mode using the [isVideoStabilizationModeSupported](#func-isvideostabilizationmodesupportedvideostabilizationmode) method.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|mode|[VideoStabilizationMode](#enum-videostabilizationmode)|Yes|-|The video stabilization mode to set.|

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required, see usage instructions
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalVideo)
    var videoSessionOption = session as VideoSession
    let videoSession = videoSessionOption.getOrThrow()
    let vsMode = VideoStabilizationMode.Off
    videoSession.setVideoStabilizationMode(vsMode)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface StabilizationQuery

```cangjie
public interface StabilizationQuery {
    func isVideoStabilizationModeSupported(vsMode: VideoStabilizationMode): Bool
}
```

**Function:** Provides the capability to query whether the device supports specified video stabilization modes during recording mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func isVideoStabilizationModeSupported(VideoStabilizationMode)

```cangjie
func isVideoStabilizationModeSupported(vsMode: VideoStabilizationMode): Bool
```

**Function:** Queries whether the specified video stabilization mode is supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|vsMode|[VideoStabilizationMode](#enum-videostabilizationmode)|Yes|-|The video stabilization mode.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns whether the video stabilization mode is supported: true for supported, false for unsupported.|

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config, only throw in session usage. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required, see usage instructions
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalVideo)
    var videoSessionOption = session as VideoSession
    let videoSession = videoSessionOption.getOrThrow()
    let vsMode = VideoStabilizationMode.Off
    videoSession.isVideoStabilizationModeSupported(vsMode)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface Zoom

```cangjie
public interface Zoom <: ZoomQuery {
    func setZoomRatio(zoomRatio: Float64): Unit
    func getZoomRatio(): Float64
    func setSmoothZoom(targetRatio: Float64, mode: SmoothZoomMode): Unit
    func setSmoothZoom(targetRatio: Float64): Unit
}
```

**Function:** Device zoom (scaling) operations.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Type:**

- [ZoomQuery](#interface-zoomquery)

### func getZoomRatio()

```cangjie
func getZoomRatio(): Float64
```

**Function:** Gets the current zoom ratio.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Float64|The current zoom ratio result.|

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required, see usage instructions
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    Hilog.info(0, "AppLogCj", photoSession.getZoomRatio().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setSmoothZoom(Float64, SmoothZoomMode)

```cangjie
func setSmoothZoom(targetRatio: Float64, mode: SmoothZoomMode): Unit
```

**Function:** Triggers smooth zoom.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|targetRatio|Float64|Yes|-|Target value.|
|mode|[SmoothZoomMode](#enum-smoothzoommode)|Yes|-|Mode.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required, see usage instructions
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let targetRatio: Float64 = 0.3
    photoSession.setSmoothZoom(targetRatio, SmoothZoomMode.Normal)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setSmoothZoom(Float64)

```cangjie
func setSmoothZoom(targetRatio: Float64): Unit
```

**Function:** Triggers smooth zoom.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|targetRatio|Float64|Yes|-|Target value.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required, see usage instructions
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let targetRatio: Float64 = 0.3
    photoSession.setSmoothZoom(targetRatio)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setZoomRatio(Float64)

```cangjie
func setZoomRatio(zoomRatio: Float64): Unit
```

**Function:** Sets the zoom ratio. The maximum precision is two decimal places. If the set value exceeds the supported precision range, only values within the precision range will be retained.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|zoomRatio|Float64|Yes|-|The zoom ratio. Use [getZoomRatioRange](#func-getzoomratiorange) to get the supported zoom range. If the set value exceeds the supported range, only values within the precision range will be retained. It takes some time for the zoom ratio to take effect at the underlying layer. Wait for 1-2 frames to get the correctly set zoom ratio.|

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required, see usage instructions
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let zoomRatio: Float64 = 0.5
    photoSession.setZoomRatio(zoomRatio)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface ZoomQuery

```cangjie
public interface ZoomQuery {
    func getZoomRatioRange(): Array<Float64>
}
```

**Function:** Provides query capabilities related to device zoom, including obtaining the supported zoom ratio range.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func getZoomRatioRange()

```cangjie
func getZoomRatioRange(): Array<Float64>
```

**Function:** Gets the supported zoom range.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Array\<Float64>|Used to obtain the zoom ratio range. The returned array includes the minimum and maximum values.|

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config, only throw in session usage. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required, see usage instructions
    let cameraManager = getCameraManager(ctx)
    let session = cameraManager.createSession(SceneMode.NormalPhoto)
    var photoSessionOption = session as PhotoSession
    let photoSession = photoSessionOption.getOrThrow()
    let zoomRatio: Float64 = 0.5
    Hilog.info(0, "AppLogCj", photoSession.getZoomRatioRange().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class CameraDevice

```cangjie
public class CameraDevice {
    public let cameraId: String
    public let cameraPosition: CameraPosition
    public let cameraType: CameraType
    public let connectionType: ConnectionType
    public let cameraOrientation: UInt32
}
```

**Description:** Camera device information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let cameraId

```cangjie
public let cameraId: String
```

**Description:** Camera ID.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let cameraOrientation

```cangjie
public let cameraOrientation: UInt32
```

**Description:** The installation angle of the camera lens, which does not change with screen rotation. Value range: 0-360.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let cameraPosition

```cangjie
public let cameraPosition: CameraPosition
```

**Description:** Camera position.

**Type:** [CameraPosition](#enum-cameraposition)

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let cameraType

```cangjie
public let cameraType: CameraType
```

**Description:** Camera type.

**Type:** [CameraType](#enum-cameratype)

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let connectionType

```cangjie
public let connectionType: ConnectionType
```

**Description:** Camera connection type.

**Type:** [ConnectionType](#enum-connectiontype)

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class CameraInput

```cangjie
public class CameraInput {}
```

**Description:** Camera device input object. Contains camera information used by the Session in a session.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func close()

```cangjie
public func close(): Unit
```

**Description:** Closes the camera.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let cameraInput = cameraManager.createCameraInput(cameraDevice)
    cameraInput.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, CameraDevice, Callback0Argument)

```cangjie
public func off(eventType: CameraEvents, camera: CameraDevice, callback: Callback0Argument): Unit
```

**Description:** Unregisters the specified callback for the specified event.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Event type to unregister. |
| camera | [CameraDevice](#class-cameradevice) | Yes | - | CameraDevice object. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let cameraInput = cameraManager.createCameraInput(cameraDevice)
    cameraInput.off(CameraEvents.CameraError, cameraDevice)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, CameraDevice)

```cangjie
public func off(eventType: CameraEvents, camera: CameraDevice): Unit
```

**Description:** Unregisters all callbacks for the specified event.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Event type to unregister. |
| camera | [CameraDevice](#class-cameradevice) | Yes | - | CameraDevice object. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let cameraInput = cameraManager.createCameraInput(cameraDevice)
    cameraInput.off(CameraEvents.CameraError, cameraDevice)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, CameraDevice, Callback0Argument)

```cangjie
public func on(eventType: CameraEvents, camera: CameraDevice, callback: Callback0Argument): Unit
```

**Description:** Listens for CameraInput error events and obtains results through registered callback functions.

> **Note:**
>
> Do not call the off method to unregister callbacks within the callback method of on.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Event type to listen for. Must be CameraError. Can be listened to after successful creation of CameraInput object. Triggers the event and returns results when the camera device encounters errors, such as unavailability or conflicts, with corresponding error messages. |
| camera | [CameraDevice](#class-cameradevice) | Yes | - | CameraDevice object. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function to obtain results. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.Callback0Argument
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added in dependency definitions
    class TestCallbackError <: Callback0Argument {
        public init() {}
        public open func invoke(res: ?BusinessException): Unit {
            Hilog.info(0, "Camera", "Call invoke error. code: ${res?.code}, msg: ${res?.message}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let cameraInput = cameraManager.createCameraInput(cameraDevice)
    let testCallbackError = TestCallbackError()
    cameraInput.on(CameraEvents.CameraError, cameraDevice, testCallbackError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func open()

```cangjie
public func open(): Unit
```

**Description:** Opens the camera.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400102 | Operation not allowed. |
  | 7400107 | Can not use camera cause of conflict. |
  | 7400108 | Camera disabled cause of security reason. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let cameraInput = cameraManager.createCameraInput(cameraDevice)
    cameraInput.open()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func open(Bool)

```cangjie
public func open(isSecureEnabled: Bool): UInt64
```

**Description:** Opens the camera and obtains the handle for a secure camera.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| isSecureEnabled | Bool | Yes | - | Whether to open the camera in secure mode. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| UInt64 | Handle of the opened camera. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400107 | Can not use camera cause of conflict. |
  | 7400108 | Camera disabled cause of security reason. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let cameraDevice = cameraManager.getSupportedCameras()[0]
    let cameraInput = cameraManager.createCameraInput(cameraDevice)
    let isSecureEnabled = false
    let handle = cameraInput.open(isSecureEnabled)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class CameraManager

```cangjie
public class CameraManager {}
```

**Description:** The camera manager class. You must call [getCameraManager](#func-getcameramanageruiabilitycontext) to obtain a camera manager instance before using this class.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func createCameraInput(CameraDevice)

```cangjie
public func createCameraInput(camera: CameraDevice): CameraInput
```

**Description:** Creates a CameraInput instance based on the camera position and type.

**Required Permission:** ohos.permission.CAMERA

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Name     | Type                          | Mandatory | Default | Description                                                                 |
| :------- | :---------------------------- | :-------- | :------ | :-------------------------------------------------------------------------- |
| camera   | [CameraDevice](#class-cameradevice) | Yes       | -       | CameraDevice object obtained via the [getSupportedCameras](#func-getsupportedcameras) API. |

**Return Value:**

| Type                          | Description          |
| :---------------------------- | :------------------- |
| [CameraInput](#class-camerainput) | CameraInput instance. |

**Exceptions:**

- BusinessException: For details about the error codes, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message                                      |
  | :----------- | :------------------------------------------------ |
  | 7400101      | Parameter missing or parameter type incorrect.    |
  | 7400102      | Operation not allowed.                            |
  | 7400201      | Camera service fatal error.                       |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Obtain the Context application context. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let cameraDevices = cameraManager.getSupportedCameras()
    let cameraDevice0 = cameraDevices[0]
    let position = cameraDevice0.cameraPosition
    let cameraType = cameraDevice0.cameraType
    let cameraInput = cameraManager.createCameraInput(position , cameraType)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func createCameraInput(CameraPosition, CameraType)

```cangjie
public func createCameraInput(position: CameraPosition, cameraType: CameraType): CameraInput
```

**Description:** Creates a CameraInput instance based on the camera position and type.

**Required Permission:** ohos.permission.CAMERA

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Name       | Type                          | Mandatory | Default | Description                                                                 |
| :--------- | :---------------------------- | :-------- | :------ | :-------------------------------------------------------------------------- |
| position   | [CameraPosition](#enum-cameraposition) | Yes       | -       | Camera position obtained via the [getSupportedCameras](#func-getsupportedcameras) API. |
| cameraType | [CameraType](#enum-cameratype) | Yes       | -       | Camera type obtained via the [getSupportedCameras](#func-getsupportedcameras) API. |

**Return Value:**

| Type                          | Description          |
| :---------------------------- | :------------------- |
| [CameraInput](#class-camerainput) | CameraInput instance. |

**Exceptions:**

- BusinessException: For details about the error codes, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message                                      |
  | :----------- | :------------------------------------------------ |
  | 7400101      | Parameter missing or parameter type incorrect.    |
  | 7400102      | Operation not allowed.                            |
  | 7400201      | Camera service fatal error.                       |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Obtain the Context application context. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let cameraDevices = cameraManager.getSupportedCameras()
    let cameraDevice0 = cameraDevices[0]
    let position = cameraDevice0.cameraPosition
    let cameraType = cameraDevice0.cameraType
    let cameraInput = cameraManager.createCameraInput(position , cameraType)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func createPhotoOutput(?Profile)

```cangjie
public func createPhotoOutput(?Profile = None): PhotoOutput
```

**Description:** Creates a photo output object.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Name    | Type                    | Mandatory | Default | Description                                                                 |
| :------ | :---------------------- | :-------- | :------ | :-------------------------------------------------------------------------- |
| profile | ?[Profile](#class-profile) | No        | None    | Supported photo configuration obtained via the [getSupportedOutputCapability](#func-getsupportedoutputcapabilitycameradevice-scenemode) API. |

**Return Value:**

| Type                    | Description         |
| :---------------------- | :------------------ |
| [PhotoOutput](#class-photooutput) | PhotoOutput instance. |

**Exceptions:**

- BusinessException: For details about the error codes, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message                                      |
  | :----------- | :------------------------------------------------ |
  | 7400101      | Parameter missing or parameter type incorrect.    |
  | 7400201      | Camera service fatal error.                       |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Obtain the Context application context. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let cameraDevices = cameraManager.getSupportedCameras()
    let camera = cameraDevices[0]
    let mode = cameraManager.getSupportedSceneModes(camera)[0]
    let cameraOutputCapability = cameraManager.getSupportedOutputCapability(camera, mode)
    let profile = cameraOutputCapability.photoProfiles[0]
    let photoOutput  = cameraManager.createPhotoOutput(profile:profile)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func createPreviewOutput(Profile, String)

```cangjie
public func createPreviewOutput(profile: Profile, surfaceId: String): PreviewOutput
```

**Description:** Creates a preview output object.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Name      | Type                    | Mandatory | Default | Description                                                                 |
| :-------- | :---------------------- | :-------- | :------ | :-------------------------------------------------------------------------- |
| profile   | [Profile](#class-profile) | Yes       | -       | Supported preview configuration obtained via the [getSupportedOutputCapability](#func-getsupportedoutputcapabilitycameradevice-scenemode) API. |
| surfaceId | String                  | Yes       | -       | surfaceId obtained from the [ImageReceiver](../ImageKit/cj-apis-image.md#class-imagereceiver) component. |

**Return Value:**

| Type                      | Description           |
| :------------------------ | :-------------------- |
| [PreviewOutput](#class-previewoutput) | PreviewOutput instance. |

**Exceptions:**

- BusinessException: For details about the error codes, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message                                      |
  | :----------- | :------------------------------------------------ |
  | 7400101      | Parameter missing or parameter type incorrect.    |
  | 7400201      | Camera service fatal error.                       |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Obtain the Context application context. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let previewOutput = cameraManager.createPreviewOutput(surfaceId)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func createPreviewOutput(String)

```cangjie
public func createPreviewOutput(surfaceId: String): PreviewOutput
```

**Description:** Creates a preview output object without configuration information. This API must be used together with [preconfig](#func-preconfigpreconfigtype-preconfigratio).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Name      | Type   | Mandatory | Default | Description                                                                 |
| :-------- | :----- | :-------- | :------ | :-------------------------------------------------------------------------- |
| surfaceId | String | Yes       | -       | surfaceId obtained from the [ImageReceiver](../ImageKit/cj-apis-image.md#class-imagereceiver) component. |

**Return Value:**

| Type                      | Description           |
| :------------------------ | :-------------------- |
| [PreviewOutput](#class-previewoutput) | PreviewOutput instance. |

**Exceptions:**

- BusinessException: For details about the error codes, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message                                      |
  | :----------- | :------------------------------------------------ |
  | 7400101      | Parameter missing or parameter type incorrect.    |
  | 7400201      | Camera service fatal error.                       |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Obtain the Context application context. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let previewOutput = cameraManager.createPreviewOutput(surfaceId)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func createSession(SceneMode)

```cangjie
public func createSession(mode: SceneMode): Session
```

**Description:** Creates a Session instance with the specified SceneMode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Name | Type                    | Mandatory | Default | Description                          |
| :--- | :---------------------- | :-------- | :------ | :----------------------------------- |
| mode | [SceneMode](#enum-scenemode) | Yes       | -       | Mode supported by the camera.        |

**Return Value:**

| Type                | Description      |
| :------------------ | :--------------- |
| [Session](#interface-session) | Session instance. |

**Exceptions:**

- BusinessException: For details about the error codes, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message                                      |
  | :----------- | :------------------------------------------------ |
  | 7400101      | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
  | 7400201      | Camera service fatal error.                       |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Obtain the Context application context. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let cameraDevices = cameraManager.getSupportedCameras()
    let camera = cameraDevices[0]
    let mode = cameraManager.getSupportedSceneModes(camera)[0]
    let session = cameraManager.createSession(mode)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func createVideoOutput(VideoProfile, String)

```cangjie
public func createVideoOutput(profile: VideoProfile, surfaceId: String): VideoOutput
```

**Description:** Creates a video output object.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Name      | Type                      | Mandatory | Default | Description                                                                 |
| :-------- | :------------------------ | :-------- | :------ | :-------------------------------------------------------------------------- |
| profile   | [VideoProfile](#class-videoprofile) | Yes       | -       | Supported video configuration obtained via the [getSupportedOutputCapability](#func-getsupportedoutputcapabilitycameradevice-scenemode) API. |
| surfaceId | String                    | Yes       | -       | surfaceId obtained from the AVRecorder.                                     |

**Return Value:**

| Type                    | Description         |
| :---------------------- | :------------------ |
| [VideoOutput](#class-videooutput) | VideoOutput instance. |

**Exceptions:**

- BusinessException: For details about the error codes, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message                                      |
  | :----------- | :------------------------------------------------ |
  | 7400101      | Parameter missing or parameter type incorrect.    |
  | 7400201      | Camera service fatal error.                       |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Obtain the Context application context. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let videoOutput = cameraManager.createVideoOutput(surfaceId)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func createVideoOutput(String)

```cangjie
public func createVideoOutput(surfaceId: String): VideoOutput
```

**Function:** Creates a video output object without configuration information. This interface must be used in conjunction with the [preconfig](#func-preconfigpreconfigtype-preconfigratio) feature.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type   | Required | Default Value | Description |
|:--------------|:-------|:---------|:--------------|:------------|
| surfaceId     | String | Yes      | -             | The surfaceId obtained from AVRecorder. |

**Return Value:**

| Type                     | Description |
|:-------------------------|:------------|
| [VideoOutput](#class-videooutput) | VideoOutput instance. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  |:-------------|:-------------|
  | 7400101      | Parameter missing or parameter type incorrect. |
  | 7400201      | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let videoOutput = cameraManager.createVideoOutput(surfaceId)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getSupportedCameras()

```cangjie
public func getSupportedCameras(): Array<CameraDevice>
```

**Function:** Retrieves the supported camera device objects.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Return Value:**

| Type                          | Description |
|:------------------------------|:------------|
| Array\<[CameraDevice](#class-cameradevice)> | List of camera devices. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let cameraDevices = cameraManager.getSupportedCameras()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getSupportedOutputCapability(CameraDevice, SceneMode)

```cangjie
public func getSupportedOutputCapability(camera: CameraDevice, mode: SceneMode): CameraOutputCapability
```

**Function:** Queries the supported output capabilities of the camera device in the specified mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type                     | Required | Default Value | Description |
|:--------------|:-------------------------|:---------|:--------------|:------------|
| camera        | [CameraDevice](#class-cameradevice) | Yes      | -             | Camera device, obtained via the [getSupportedCameras](#func-getsupportedcameras) interface. |
| mode          | [SceneMode](#enum-scenemode) | Yes      | -             | Camera mode, obtained via the [getSupportedSceneModes](#func-getsupportedscenemodescameradevice) interface. |

**Return Value:**

| Type                               | Description |
|:-----------------------------------|:------------|
| [CameraOutputCapability](#class-cameraoutputcapability) | Camera output capability. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let cameraDevices = cameraManager.getSupportedCameras()
    let camera = cameraDevices[0]
    let mode = cameraManager.getSupportedSceneModes(camera)[0]
    let cameraOutputCapability = cameraManager.getSupportedOutputCapability(camera, mode)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getSupportedSceneModes(CameraDevice)

```cangjie
public func getSupportedSceneModes(camera: CameraDevice): Array<SceneMode>
```

**Function:** Retrieves the supported modes of the specified camera device object.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type                     | Required | Default Value | Description |
|:--------------|:-------------------------|:---------|:--------------|:------------|
| camera        | [CameraDevice](#class-cameradevice) | Yes      | -             | Camera device, obtained via the [getSupportedCameras](#func-getsupportedcameras) interface. |

**Return Value:**

| Type                     | Description |
|:-------------------------|:------------|
| Array\<[SceneMode](#enum-scenemode)> | List of supported camera modes. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let cameraDevices = cameraManager.getSupportedCameras()
    let camera = cameraDevices[0]
    let mode = cameraManager.getSupportedSceneModes(camera)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getTorchMode()

```cangjie
public func getTorchMode(): TorchMode
```

**Function:** Retrieves the current torch mode of the device.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Return Value:**

| Type               | Description |
|:-------------------|:------------|
| [TorchMode](#enum-torchmode) | Current torch mode of the device. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let torchMode = cameraManager.getTorchMode()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isCameraMuted()

```cangjie
public func isCameraMuted(): Bool
```

**Function:** Queries the current disabled status of the camera (disabled/enabled).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:-----|:------------|
| Bool | Returns `true` if the camera is disabled, `false` otherwise. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    Hilog.info(0, "AppLogCj", cameraManager.isCameraMuted().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isTorchModeSupported(TorchMode)

```cangjie
public func isTorchModeSupported(mode: TorchMode): Bool
```

**Function:** Checks whether the specified torch mode is supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type               | Required | Default Value | Description |
|:--------------|:-------------------|:---------|:--------------|:------------|
| mode          | [TorchMode](#enum-torchmode) | Yes      | -             | Torch mode. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| Bool | Returns `true` if the device supports the specified torch mode. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let torchMode = cameraManager.getTorchMode()
    Hilog.info(0, "AppLogCj", cameraManager.isTorchModeSupported(torchMode).toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isTorchSupported()

```cangjie
public func isTorchSupported(): Bool
```

**Function:** Checks whether the device supports torch.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:-----|:------------|
| Bool | Returns `true` if the device supports torch. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    Hilog.info(0, "AppLogCj", cameraManager.isTorchSupported().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback1Argument\<CameraStatusInfo>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<CameraStatusInfo>): Unit
```

**Function:** Unregisters the camera device status callback, cancelling the retrieval of camera status changes via the callback function.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type                                     | Required | Default Value | Description |
|:--------------|:-----------------------------------------|:---------|:--------------|:------------|
| eventType     | [CameraEvents](#enum-cameraevents)       | Yes      | -             | Event to listen for, must be `CameraStatus`. Can be monitored after the CameraManager object is successfully obtained. Currently, only device opening or closing triggers this event and returns corresponding information. |
| callback      | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[CameraStatusInfo](#class-camerastatusinfo)> | Yes      | -             | Callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  |:-------------|:-------------|
  | 7400201      | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    cameraManager.off(CameraEvents.TorchStatusChange)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback1Argument\<FoldStatusInfo>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<FoldStatusInfo>): Unit
```

**Function:** Unregisters the fold status change callback for foldable devices, cancelling the retrieval of fold status changes via the callback function.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type                                     | Required | Default Value | Description |
|:--------------|:-----------------------------------------|:---------|:--------------|:------------|
| eventType     | [CameraEvents](#enum-cameraevents)       | Yes      | -             | Event to listen for, must be `FoldStatusChange`. Indicates a change in the fold status of a foldable device. |
| callback      | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[FoldStatusInfo](#class-foldstatusinfo)> | Yes      | -             | Callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  |:-------------|:-------------|
  | 7400201      | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. For details, see the usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    cameraManager.off(CameraEvents.TorchStatusChange)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func off(CameraEvents, Callback1Argument\<TorchStatusInfo>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<TorchStatusInfo>): Unit
```

**Function:** Unregisters the callback for torch status changes by removing the callback function that receives torch status updates.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to unlisten for, must be TorchStatusChange. Can be monitored after successfully obtaining the CameraManager object. Currently only supports torch on, torch off, torch unavailable, and torch becoming available events which trigger this callback with corresponding information. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[TorchStatusInfo](#class-torchstatusinfo)> | Yes | - | The callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    cameraManager.off(CameraEvents.TorchStatusChange)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents)

```cangjie
public func off(eventType: CameraEvents): Unit
```

**Function:** Cancels all callbacks for the specified event type.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event type to unlisten for. Must be an event that can be registered via the on() function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    cameraManager.off(CameraEvents.TorchStatusChange)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback1Argument\<CameraStatusInfo>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<CameraStatusInfo>): Unit
```

**Function:** Registers a callback for camera device status changes. Uses asynchronous callback via the callback parameter.

> **Note:**
>
> Calling off() to unregister callbacks within an on() callback method is not supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, must be CameraStatus. Can be monitored after successfully obtaining the CameraManager object. Currently only supports camera device open/close events which trigger this callback with corresponding information. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[CameraStatusInfo](#class-camerastatusinfo)> | Yes | - | The callback function that receives camera status change information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.Callback1Argument
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class TestCallbackTorchStatusChange <: Callback1Argument<TorchStatusInfo> {
        public init() {}
        public open func invoke(err: ?BusinessException, res: TorchStatusInfo): Unit {
            Hilog.info(0, "Camera", "Call invoke TorchStatusChange. isTorchAvailable: ${res.isTorchAvailable}, isTorchActive: ${res.isTorchActive}, torchLevel:${res.torchLevel}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let testCallbackTorchStatusChange = TestCallbackTorchStatusChange()
    cameraManager.on(CameraEvents.TorchStatusChange, testCallbackTorchStatusChange)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback1Argument\<FoldStatusInfo>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<FoldStatusInfo>): Unit
```

**Function:** Registers a listener for foldable device folding status changes.

> **Note:**
>
> Calling off() to unregister callbacks within an on() callback method is not supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, must be FoldStatusChange. Indicates foldable device folding status changes. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[FoldStatusInfo](#class-foldstatusinfo)> | Yes | - | The callback function that returns foldable device folding information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.Callback1Argument
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class TestCallbackTorchStatusChange <: Callback1Argument<TorchStatusInfo> {
        public init() {}
        public open func invoke(err: ?BusinessException, res: TorchStatusInfo): Unit {
            Hilog.info(0, "Camera", "Call invoke TorchStatusChange. isTorchAvailable: ${res.isTorchAvailable}, isTorchActive: ${res.isTorchActive}, torchLevel:${res.torchLevel}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let testCallbackTorchStatusChange = TestCallbackTorchStatusChange()
    cameraManager.on(CameraEvents.TorchStatusChange, testCallbackTorchStatusChange)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback1Argument\<TorchStatusInfo>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<TorchStatusInfo>): Unit
```

**Function:** Registers a callback for torch status changes.

> **Note:**
>
> Calling off() to unregister callbacks within an on() callback method is not supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, must be TorchStatusChange. Can be monitored after successfully obtaining the cameraManager object. Currently only supports torch on, torch off, torch unavailable, and torch becoming available events which trigger this callback with corresponding information. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[TorchStatusInfo](#class-torchstatusinfo)> | Yes | - | The callback function that receives torch status change information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.Callback1Argument
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class TestCallbackTorchStatusChange <: Callback1Argument<TorchStatusInfo> {
        public init() {}
        public open func invoke(err: ?BusinessException, res: TorchStatusInfo): Unit {
            Hilog.info(0, "Camera", "Call invoke TorchStatusChange. isTorchAvailable: ${res.isTorchAvailable}, isTorchActive: ${res.isTorchActive}, torchLevel:${res.torchLevel}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let testCallbackTorchStatusChange = TestCallbackTorchStatusChange()
    cameraManager.on(CameraEvents.TorchStatusChange, testCallbackTorchStatusChange)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setTorchMode(TorchMode)

```cangjie
public func setTorchMode(mode: TorchMode): Unit
```

**Function:** Sets the device's torch mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| mode | [TorchMode](#enum-torchmode) | Yes | - | The torch mode to set. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400102 | Operation not allowed. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    cameraManager.setTorchMode(TorchMode.On)
    cameraManager.setTorchMode(TorchMode.Off)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class CameraOutputCapability

```cangjie
public class CameraOutputCapability {
    public let previewProfiles: Array<Profile>
    public let photoProfiles: Array<Profile>
    public let videoProfiles: Array<VideoProfile>
    public let supportedMetadataObjectTypes: Array<MetadataObjectType>
}
```

**Function:** Camera output capability items.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let photoProfiles

```cangjie
public let photoProfiles: Array<Profile>
```

**Function:** Collection of supported photo configuration profiles.

**Type:** Array\<[Profile](#class-profile)>

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let previewProfiles

```cangjie
public let previewProfiles: Array<Profile>
```

**Function:** Collection of supported preview configuration profiles.

**Type:** Array\<[Profile](#class-profile)>

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let supportedMetadataObjectTypes

```cangjie
public let supportedMetadataObjectTypes: Array<MetadataObjectType>
```

**Function:** Collection of supported metadata stream types.

**Type:** Array\<[MetadataObjectType](#enum-metadataobjecttype)>

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let videoProfiles

```cangjie
public let videoProfiles: Array<VideoProfile>
```

**Function:** Collection of supported video recording configuration profiles.

**Type:** Array\<[VideoProfile](#class-videoprofile)>

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22## class CameraStatusInfo

```cangjie
public class CameraStatusInfo {
    public var camera: CameraDevice
    public var status: CameraStatus
}
```

**Function:** An interface instance returned by the camera manager callback, representing camera status information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var camera

```cangjie
public var camera: CameraDevice
```

**Function:** Camera information.

**Type:** [CameraDevice](#class-cameradevice)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var status

```cangjie
public var status: CameraStatus
```

**Function:** Camera status.

**Type:** [CameraStatus](#enum-camerastatus)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class CaptureEndInfo

```cangjie
public class CaptureEndInfo {
    public var captureId: Int32
    public var frameCount: Int32
}
```

**Function:** Photo capture stop information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var captureId

```cangjie
public var captureId: Int32
```

**Function:** Photo capture ID.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var frameCount

```cangjie
public var frameCount: Int32
```

**Function:** Frame count.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class CaptureStartInfo

```cangjie
public class CaptureStartInfo {
    public var captureId: Int32
    public var time: Int64
}
```

**Function:** Photo capture start information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var captureId

```cangjie
public var captureId: Int32
```

**Function:** Photo capture ID.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var time

```cangjie
public var time: Int64
```

**Function:** Estimated single photo capture time for sensor frame collection at the underlying layer.

**Type:** Int64

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class FoldStatusInfo

```cangjie
public class FoldStatusInfo {
    public let supportedCameras: Array<CameraDevice>
    public let foldStatus: FoldStatus
}
```

**Function:** An interface instance returned by the camera manager callback, representing foldable device folding status information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let foldStatus

```cangjie
public let foldStatus: FoldStatus
```

**Function:** Foldable screen folding status.

**Type:** [FoldStatus](#enum-foldstatus)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let supportedCameras

```cangjie
public let supportedCameras: Array<CameraDevice>
```

**Function:** List of supported camera information under the current folding status.

**Type:** Array\<[CameraDevice](#class-cameradevice)>

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class FrameRateRange

```cangjie
public class FrameRateRange {
    public let min: Int32
    public let max: Int32
}
```

**Function:** Frame rate range.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let max

```cangjie
public let max: Int32
```

**Function:** Maximum frame rate.

**Type:** Int32

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let min

```cangjie
public let min: Int32
```

**Function:** Minimum frame rate.

**Type:** Int32

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class FrameShutterEndInfo

```cangjie
public class FrameShutterEndInfo {
    public var captureId: Int32
}
```

**Function:** Photo exposure end information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var captureId

```cangjie
public var captureId: Int32
```

**Function:** Photo capture ID.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class FrameShutterInfo

```cangjie
public class FrameShutterInfo {
    public var captureId: Int32
    public var timestamp: Int64
}
```

**Function:** Photo frame output information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var captureId

```cangjie
public var captureId: Int32
```

**Function:** Photo capture ID.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var timestamp

```cangjie
public var timestamp: Int64
```

**Function:** Shutter timestamp.

**Type:** Int64

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class Location

```cangjie
public class Location {
    public var latitude: Float64
    public var longitude: Float64
    public var altitude: Float64
    public init(latitude: Float64, longitude: Float64, altitude: Float64)
}
```

**Function:** Image geographical location information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var altitude

```cangjie
public var altitude: Float64
```

**Function:** Altitude (meters).

**Type:** Float64

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var latitude

```cangjie
public var latitude: Float64
```

**Function:** Latitude (degrees).

**Type:** Float64

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var longitude

```cangjie
public var longitude: Float64
```

**Function:** Longitude (degrees).

**Type:** Float64

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### init(Float64, Float64, Float64)

```cangjie
public init(latitude: Float64, longitude: Float64, altitude: Float64)
```

**Function:** Creates a Location object.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type    | Required | Default | Description            |
|:----------|:--------|:---------|:--------|:-----------------------|
| latitude  | Float64 | Yes      | -       | Latitude (degrees).    |
| longitude | Float64 | Yes      | -       | Longitude (degrees).   |
| altitude  | Float64 | Yes      | -       | Altitude (meters).     |

## class PhotoCaptureSetting

```cangjie
public class PhotoCaptureSetting {
    public var quality: QualityLevel
    public var rotation: ImageRotation
    public var location:?Location
    public var mirror: Bool
    public init(
        quality!: QualityLevel = QualityLevel.QualityLevelLow,
        rotation!: ImageRotation = ImageRotation.Rotation0,
        location!: ?Location = None,
        mirror!: Bool = false
    )
}
```

**Function:** Settings for capturing photos.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var location

```cangjie
public var location:?Location
```

**Function:** Image geographical location information (defaults to device hardware information).

**Type:** ?[Location](#class-location)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var mirror

```cangjie
public var mirror: Bool
```

**Function:** Mirror enable switch (default off). Use [isMirrorSupported](#func-ismirrorsupported) to check support before using.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var quality

```cangjie
public var quality: QualityLevel
```

**Function:** Image quality (default low).

**Type:** [QualityLevel](#enum-qualitylevel)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var rotation

```cangjie
public var rotation: ImageRotation
```

**Function:** Image rotation angle (default 0 degrees, clockwise rotation).

**Type:** [ImageRotation](#enum-imagerotation)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### init(QualityLevel, ImageRotation, ?Location, Bool)

```cangjie
public init(
    quality!: QualityLevel = QualityLevel.QualityLevelLow,
    rotation!: ImageRotation = ImageRotation.Rotation0,
    location!: ?Location = None,
    mirror!: Bool = false
)
```

**Function:** Creates a PhotoCaptureSetting object.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type                     | Required | Default                    | Description                                                                 |
|:----------|:-------------------------|:---------|:---------------------------|:----------------------------------------------------------------------------|
| quality   | [QualityLevel](#enum-qualitylevel) | No       | QualityLevel.QualityLevelLow | **Named parameter.** Image quality (default low).                          |
| rotation  | [ImageRotation](#enum-imagerotation) | No       | ImageRotation.Rotation0     | **Named parameter.** Image rotation angle (default 0 degrees).             |
| location  | ?[Location](#class-location)         | No       | None                       | **Named parameter.** Image geographical location information (defaults to device hardware information). |
| mirror    | Bool                     | No       | false                      | **Named parameter.** Mirror enable switch (default off). Use [isMirrorSupported](#func-ismirrorsupported) to check support before using. |## class PhotoOutput

```cangjie
public class PhotoOutput CameraOutput {}
```

**Function:** Output information used in photo capture sessions.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Type:**

- [CameraOutput](#interface-cameraoutput)

### func capture()

```cangjie
public func capture(): Unit
```

**Function:** Triggers a single photo capture with specified parameters.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400104 | Session not running. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    output.capture(PhotoCaptureSetting())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func capture(PhotoCaptureSetting)

```cangjie
public func capture(setting: PhotoCaptureSetting): Unit
```

**Function:** Triggers a single photo capture with specified parameters.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| setting | [PhotoCaptureSetting](#class-photocapturesetting) | Yes | - | Photo capture settings. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400104 | Session not running. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    output.capture(PhotoCaptureSetting())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func enableMirror(Bool)

```cangjie
public func enableMirror(enabled: Bool): Unit
```

**Function:** Enables or disables mirror photo capture.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| enabled | Bool | Yes | - | `true` to enable mirror photo capture, `false` to disable. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400103 | Session not config. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    let enabled = true
    output.enableMirror(enabled)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func enableMovingPhoto(Bool)

```cangjie
public func enableMovingPhoto(enabled: Bool): Unit
```

**Function:** Enables or disables moving photo capture.

**Required Permission:** ohos.permission.MICROPHONE

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| enabled | Bool | Yes | - | `true` to enable moving photo, `false` to disable. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | permission denied. |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    let enabled = true
    output.enableMovingPhoto(enabled)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getActiveProfile()

```cangjie
public func getActiveProfile(): Profile
```

**Function:** Retrieves the currently active configuration information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| [Profile](#class-profile) | Currently active configuration information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    let profile = output.getActiveProfile()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getPhotoRotation(Int32)

```cangjie
public func getPhotoRotation(deviceDegree: Int32): ImageRotation
```

**Function:** Retrieves the photo rotation angle.

- Device natural orientation: Default usage orientation of the device. For mobile phones, this is portrait mode (charging port facing downward).
- Camera lens angle: Value equals the clockwise rotation angle from the camera image to the device's natural orientation. The rear camera sensor of a mobile phone is installed in portrait mode, so it needs to be rotated 90 degrees clockwise to align with the device's natural orientation.
- Screen display orientation: The top-left corner of the displayed image should be the coordinate origin (first pixel point). When locked, it aligns with the natural orientation.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| deviceDegree | Int32 | Yes | - | Device rotation angle. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [ImageRotation](#enum-imagerotation) | Photo rotation angle. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    let deviceDegree: Int32 = 0
    let imageRotation = output.getPhotoRotation(deviceDegree)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getSupportedMovingPhotoVideoCodecTypes()

```cangjie
public func getSupportedMovingPhotoVideoCodecTypes(): Array<VideoCodecType>
```

**Function:** Queries supported video codec types for moving photos.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<[VideoCodecType](#enum-videocodectype)> | List of supported video codec types for moving photos. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    let videoCodecTypes = output.getSupportedMovingPhotoVideoCodecTypes()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isMirrorSupported()

```cangjie
public func isMirrorSupported(): Bool
```

**Function:** Queries whether mirror photo capture is supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns whether mirror photo capture is supported. `true` indicates support, `false` indicates no support. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    Hilog.info(0, "AppLogCj", output.isMirrorSupported().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func isMovingPhotoSupported()

```cangjie
public func isMovingPhotoSupported(): Bool
```

**Function:** Queries whether moving photo capture is supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns whether moving photo capture is supported. true indicates supported, false indicates not supported. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    Hilog.info(0, "AppLogCj", output.isMovingPhotoSupported().toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback1Argument\<CaptureStartInfo>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<CaptureStartInfo>): Unit
```

**Function:** Unregisters the listener for photo capture.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be CaptureStartWithInfo. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[CaptureStartInfo](#class-capturestartinfo)> | Yes | - | Callback function for handling [CaptureStartInfo](#class-capturestartinfo). |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    output.off(CameraEvents.CaptureStartWithInfo)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback1Argument\<FrameShutterInfo>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<FrameShutterInfo>): Unit
```

**Function:** Unregisters the listener for photo frame output capture.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be FrameShutter. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[FrameShutterInfo](#class-frameshutterinfo)> | Yes | - | Callback function for handling [FrameShutterInfo](#class-frameshutterinfo). |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    output.off(CameraEvents.CaptureStartWithInfo)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback1Argument\<CaptureEndInfo>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<CaptureEndInfo>): Unit
```

**Function:** Unregisters the listener for photo capture completion.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be CaptureEnd. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[CaptureEndInfo](#class-captureendinfo)> | Yes | - | Callback function for handling [CaptureEndInfo](#class-captureendinfo). |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    output.off(CameraEvents.CaptureStartWithInfo)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback1Argument\<FrameShutterEndInfo>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<FrameShutterEndInfo>): Unit
```

**Function:** Unregisters the listener for photo frame output capture.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be FrameShutterEnd. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[FrameShutterEndInfo](#class-frameshutterendinfo)> | Yes | - | Callback function for handling [FrameShutterEndInfo](#class-frameshutterendinfo). |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    output.off(CameraEvents.CaptureStartWithInfo)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback0Argument)

```cangjie
public func off(eventType: CameraEvents, callback: Callback0Argument): Unit
```

**Function:** Unregisters the listener for next capture readiness or error.

**System Capability:** SystemCapability.MMultimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be one of [CaptureReady, CameraError]. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    output.off(CameraEvents.CaptureStartWithInfo)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback1Argument\<Float64>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<Float64>): Unit
```

**Function:** Unregisters the listener for estimated capture duration.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be EstimatedCaptureDuration. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<Float64> | Yes | - | Callback function for obtaining estimated capture duration (in milliseconds). |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    output.off(CameraEvents.CaptureStartWithInfo)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents)

```cangjie
public func off(eventType: CameraEvents): Unit
```

**Function:** Cancels all callbacks for the specified listening event.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event. Must be an event that can be listened to by the on function. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    output.off(CameraEvents.CaptureStartWithInfo)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func on(CameraEvents, Callback1Argument\<CaptureStartInfo>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<CaptureStartInfo>): Unit
```

**Function:** Listens for photo capture start events by registering a callback function to obtain CaptureStartInfo. Uses asynchronous callback via `callback`.

> **Note:**
>
> It is not supported to call `off` to unregister the callback within the callback method registered via `on`.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, must be `CaptureStartWithInfo`. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[CaptureStartInfo](#class-capturestartinfo)> | Yes | - | Callback function for handling [CaptureStartInfo](#class-capturestartinfo). |

**Exceptions:**

- BusinessException: Error codes as listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.Callback0Argument
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class TestCallbackError <: Callback0Argument {
        public init() {}
        public open func invoke(res: ?BusinessException): Unit {
            Hilog.info(0, "Camera", "Call invoke error. code: ${res?.code}, msg: ${res?.message}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required, see usage notes
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    let testCallbackError = TestCallbackError()
    output.on(CameraEvents.CameraError, testCallbackError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback1Argument\<FrameShutterInfo>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<FrameShutterInfo>): Unit
```

**Function:** Listens for photo frame output capture events by registering a callback function to obtain results. Uses asynchronous callback via `callback`.

> **Note:**
>
> It is not supported to call `off` to unregister the callback within the callback method registered via `on`.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, must be `FrameShutter`. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[FrameShutterInfo](#class-frameshutterinfo)> | Yes | - | Callback function for handling [FrameShutterInfo](#class-frameshutterinfo). |

**Exceptions:**

- BusinessException: Error codes as listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.Callback0Argument
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class TestCallbackError <: Callback0Argument {
        public init() {}
        public open func invoke(res: ?BusinessException): Unit {
            Hilog.info(0, "Camera", "Call invoke error. code: ${res?.code}, msg: ${res?.message}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required, see usage notes
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    let testCallbackError = TestCallbackError()
    output.on(CameraEvents.CameraError, testCallbackError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback1Argument\<CaptureEndInfo>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<CaptureEndInfo>): Unit
```

**Function:** Listens for photo capture end events by registering a callback function to obtain results. Uses asynchronous callback via `callback`.

> **Note:**
>
> It is not supported to call `off` to unregister the callback within the callback method registered via `on`.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, must be `CaptureEnd`. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[CaptureEndInfo](#class-captureendinfo)> | Yes | - | Callback function for handling [CaptureEndInfo](#class-captureendinfo). |

**Exceptions:**

- BusinessException: Error codes as listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.Callback0Argument
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class TestCallbackError <: Callback0Argument {
        public init() {}
        public open func invoke(res: ?BusinessException): Unit {
            Hilog.info(0, "Camera", "Call invoke error. code: ${res?.code}, msg: ${res?.message}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required, see usage notes
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    let testCallbackError = TestCallbackError()
    output.on(CameraEvents.CameraError, testCallbackError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback1Argument\<FrameShutterEndInfo>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<FrameShutterEndInfo>): Unit
```

**Function:** Listens for photo frame output capture events by registering a callback function to obtain results. Uses asynchronous callback via `callback`.

> **Note:**
>
> It is not supported to call `off` to unregister the callback within the callback method registered via `on`.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, must be `FrameShutterEnd`. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[FrameShutterEndInfo](#class-frameshutterendinfo)> | Yes | - | Callback function for handling [FrameShutterEndInfo](#class-frameshutterendinfo). |

**Exceptions:**

- BusinessException: Error codes as listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.Callback0Argument
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class TestCallbackError <: Callback0Argument {
        public init() {}
        public open func invoke(res: ?BusinessException): Unit {
            Hilog.info(0, "Camera", "Call invoke error. code: ${res?.code}, msg: ${res?.message}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required, see usage notes
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    let testCallbackError = TestCallbackError()
    output.on(CameraEvents.CameraError, testCallbackError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback0Argument)

```cangjie
public func on(eventType: CameraEvents, callback: Callback0Argument): Unit
```

**Function:** Listens for readiness to capture the next photo or photo capture errors by registering a callback function to obtain results. Uses asynchronous callback via `callback`.

> **Note:**
>
> It is not supported to call `off` to unregister the callback within the callback method registered via `on`.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, must be one of `[CaptureReady, CameraError]`. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function. |

**Exceptions:**

- BusinessException: Error codes as listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.Callback0Argument
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class TestCallbackError <: Callback0Argument {
        public init() {}
        public open func invoke(res: ?BusinessException): Unit {
            Hilog.info(0, "Camera", "Call invoke error. code: ${res?.code}, msg: ${res?.message}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required, see usage notes
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    let testCallbackError = TestCallbackError()
    output.on(CameraEvents.CameraError, testCallbackError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback1Argument\<Float64>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<Float64>): Unit
```

**Function:** Listens for estimated photo capture duration by registering a callback function to obtain results. Uses asynchronous callback via `callback`.

> **Note:**
>
> It is not supported to call `off` to unregister the callback within the callback method registered via `on`.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, must be `EstimatedCaptureDuration`. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<Float64> | Yes | - | Callback function for obtaining estimated photo capture duration (in milliseconds). |

**Exceptions:**

- BusinessException: Error codes as listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.Callback0Argument
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class TestCallbackError <: Callback0Argument {
        public init() {}
        public open func invoke(res: ?BusinessException): Unit {
            Hilog.info(0, "Camera", "Call invoke error. code: ${res?.code}, msg: ${res?.message}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required, see usage notes
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    let testCallbackError = TestCallbackError()
    output.on(CameraEvents.CameraError, testCallbackError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func release()

```cangjie
public func release(): Unit
```

**Function:** Releases output resources.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Exceptions:**

- BusinessException: Error codes as listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required, see usage notes
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProfiles[0])
    output.release()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setMovingPhotoVideoCodecType(VideoCodecType)

```cangjie
public func setMovingPhotoVideoCodecType(codecType: VideoCodecType): Unit
```

**Function:** Sets the video codec type for moving photos (short videos).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| codecType | [VideoCodecType](#enum-videocodectype) | Yes | - | The video codec type for moving photos. |

**Exceptions:**

- BusinessException: Error codes as listed below. See [Camera Error Codes](./cj-errorcode-multimedia-camera.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required, see usage notes
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let output = cameraManager.createPhotoOutput(profile:ability.photoProf## class PhotoSession

```cangjie
public class PhotoSession  Session & Flash & AutoExposure & Focus & Zoom & ColorManagement {}
```

**Description:** A standard photo capture session class that provides operations for flash, exposure, focus, zoom, and color space management.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Inherits From:**

- [Session](#interface-session)
- [Flash](#interface-flash)
- [AutoExposure](#interface-autoexposure)
- [Focus](#interface-focus)
- [Zoom](#interface-zoom)
- [ColorManagement](#interface-colormanagement)

### func canPreconfig(PreconfigType, PreconfigRatio)

```cangjie
public func canPreconfig(preconfigType: PreconfigType, preconfigRatio!: PreconfigRatio = PreconfigRatio_4_3): Bool
```

**Description:** Queries whether the current session supports the specified preconfiguration type.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| preconfigType | [PreconfigType](#enum-preconfigtype) | Yes | - | Specifies the expected resolution configuration. |
| preconfigRatio | [PreconfigRatio](#enum-preconfigratio) | No | PreconfigRatio_4_3 | **Named parameter.** Optional aspect ratio. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: Supports the specified preconfiguration type. false: Does not support the specified preconfiguration type. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let photoSession = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
    let session = photoSession.getOrThrow()
    Hilog.info(0, "AppLogCj", session.canPreconfig(Preconfig1080p, preconfigRatio: PreconfigRatio_16_9).toString())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback0Argument)

```cangjie
public func off(eventType: CameraEvents, callback: Callback0Argument): Unit
```

**Description:** Unregisters the listener for error events in a standard photo capture session. Results are obtained through the registered callback function.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, which must be CameraError. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function for handling [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception). |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let photoSession = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
    let session = photoSession.getOrThrow()
    session.off(CameraEvents.FocusStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback1Argument\<FocusState>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<FocusState>): Unit
```

**Description:** Unregisters the listener for camera focus state changes.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, which must be FocusStateChange. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[FocusState](#enum-focusstate)> | Yes | - | Callback function for handling [FocusState](#enum-focusstate). |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let photoSession = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
    let session = photoSession.getOrThrow()
    session.off(CameraEvents.FocusStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback1Argument\<SmoothZoomInfo>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<SmoothZoomInfo>): Unit
```

**Description:** Unregisters the listener for camera smooth zoom state changes.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, which must be SmoothZoomInfoAvailable. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[SmoothZoomInfo](#class-smoothzoominfo)> | Yes | - | Callback function for handling [SmoothZoomInfo](#class-smoothzoominfo). |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let photoSession = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
    let session = photoSession.getOrThrow()
    session.off(CameraEvents.FocusStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents)

```cangjie
public func off(eventType: CameraEvents): Unit
```

**Description:** Unregisters the listener for error events in a standard photo capture session, camera focus state changes, or camera smooth zoom state changes.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for. Must be an event that can be registered via the `on` function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let photoSession = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
    let session = photoSession.getOrThrow()
    session.off(CameraEvents.FocusStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback0Argument)

```cangjie
public func on(eventType: CameraEvents, callback: Callback0Argument): Unit
```

**Description:** Listens for error events in a standard photo capture session. Results are obtained through the registered callback function. Uses callback for asynchronous results.

> **Note:**
>
> Calling `off` to unregister the callback within the `on` listener callback method is not supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, which must be CameraError. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function for handling [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception). |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.*
import ohos.business_exception.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class SmoothZoomInfoAvailableCallback <: Callback1Argument<SmoothZoomInfo> {
        public static var invoked = false

        public func invoke(err: ?BusinessException, info: SmoothZoomInfo) {
            Hilog.info(0, "AppLogCj", "[multimedia_camera | SmoothZoomInfoAvailable Callback]: info: ${info.duration}")

            invoked = true
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let photoSession = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
    let session = photoSession.getOrThrow()
    let callback = SmoothZoomInfoAvailableCallback()
    session.on(CameraEvents.SmoothZoomInfoAvailable, callback)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback1Argument\<FocusState>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<FocusState>): Unit
```

**Description:** Listens for camera focus state changes. Results are obtained through the registered callback function. Uses callback for asynchronous results.

> **Note:**
>
> Calling `off` to unregister the callback within the `on` listener callback method is not supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, which must be FocusStateChange. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[FocusState](#enum-focusstate)> | Yes | - | Callback function for obtaining the current focus state. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.*
import ohos.business_exception.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class SmoothZoomInfoAvailableCallback <: Callback1Argument<SmoothZoomInfo> {
        public static var invoked = false

        public func invoke(err: ?BusinessException, info: SmoothZoomInfo) {
            Hilog.info(0, "AppLogCj", "[multimedia_camera | SmoothZoomInfoAvailable Callback]: info: ${info.duration}")

            invoked = true
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let photoSession = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
    let session = photoSession.getOrThrow()
    let callback = SmoothZoomInfoAvailableCallback()
    session.on(CameraEvents.SmoothZoomInfoAvailable, callback)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback1Argument\<SmoothZoomInfo>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<SmoothZoomInfo>): Unit
```

**Description:** Listens for camera smooth zoom state changes. Results are obtained through the registered callback function. Uses callback for asynchronous results.

> **Note:**
>
> Calling `off` to unregister the callback within the `on` listener callback method is not supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for, which must be SmoothZoomInfoAvailable. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[SmoothZoomInfo](#class-smoothzoominfo)> | Yes | - | Callback function for handling [SmoothZoomInfo](#class-smoothzoominfo). |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.*
import ohos.business_exception.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class SmoothZoomInfoAvailableCallback <: Callback1Argument<SmoothZoomInfo> {
        public static var invoked = false

        public func invoke(err: ?BusinessException, info: SmoothZoomInfo) {
            Hilog.info(0, "AppLogCj", "[multimedia_camera | SmoothZoomInfoAvailable Callback]: info: ${info.duration}")

            invoked = true
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let photoSession = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
    let session = photoSession.getOrThrow()
    let callback = SmoothZoomInfoAvailableCallback()
    session.on(CameraEvents.SmoothZoomInfoAvailable, callback)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func preconfig(PreconfigType, PreconfigRatio)

```cangjie
public func preconfig(
    preconfigType: PreconfigType,
    preconfigRatio!: PreconfigRatio = PreconfigRatio.PreconfigRatio_4_3
): Unit
```

**Description:** Preconfigures the current session.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| preconfigType | [PreconfigType](#enum-preconfigtype) | Yes | - | Specifies the expected resolution configuration. |
| preconfigRatio | [PreconfigRatio](#enum-preconfigratio) | No | PreconfigRatio.PreconfigRatio_4_3 | **Named parameter.** Optional aspect ratio. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let photoSession = cameraManager.createSession(SceneMode.NormalPhoto) as PhotoSession
    let session = photoSession.getOrThrow()
    session.preconfig(Preconfig1080p, preconfigRatio: PreconfigRatio_16_9)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class Point

```cangjie
public class Point {
    public var x: Float64
    public var y: Float64
    public init(x: Float64, y: Float64)
}
```

**Function:** Point coordinates used for focus and exposure configuration.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var x

```cangjie
public var x: Float64
```

**Function:** The x-coordinate of the point.

**Type:** Float64

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var y

```cangjie
public var y: Float64
```

**Function:** The y-coordinate of the point.

**Type:** Float64

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### init(Float64, Float64)

```cangjie
public init(x: Float64, y: Float64)
```

**Function:** Creates a Point object.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | Float64 | Yes | - | The x-coordinate of the point. |
| y | Float64 | Yes | - | The y-coordinate of the point. |

## class PreviewOutput

```cangjie
public class PreviewOutput  CameraOutput {}
```

**Function:** Preview output class.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Type:**

- [CameraOutput](#interface-cameraoutput)

### func getActiveFrameRate()

```cangjie
public func getActiveFrameRate(): FrameRateRange
```

**Function:** Gets the configured frame rate range.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [FrameRateRange](#class-frameraterange) | The frame rate range. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createPreviewOutput(ability.previewProfiles[0], surfaceId)
    let range = output.getActiveFrameRate()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getActiveProfile()

```cangjie
public func getActiveProfile(): Profile
```

**Function:** Gets the currently active configuration information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Profile](#class-profile) | The currently active configuration information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createPreviewOutput(ability.previewProfiles[0], surfaceId)
    let profile = output.getActiveProfile()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getPreviewRotation(Int32)

```cangjie
public func getPreviewRotation(displayRotation: Int32): ImageRotation
```

**Function:** Gets the preview rotation angle.

- Device natural orientation: The default usage orientation of the device. For mobile phones, it is portrait (charging port facing downward).
- Camera lens angle: The value equals the angle by which the camera image is rotated clockwise to align with the device's natural orientation. For mobile phone rear cameras, the sensor is installed in portrait mode, so it needs to be rotated 90 degrees clockwise to align with the device's natural orientation.
- Screen display orientation: The image displayed on the screen should have its top-left corner as the origin (0,0) of the coordinate system. When the screen is locked, it aligns with the natural orientation.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| displayRotation | Int32 | Yes | - | The screen rotation angle of the display device, obtained via [getDefaultDisplaySync](../arkui-cj/cj-apis-display.md#func-getdefaultdisplaysync). |

**Return Value:**

| Type | Description |
|:----|:----|
| [ImageRotation](#enum-imagerotation) | The preview rotation angle. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createPreviewOutput(ability.previewProfiles[0], surfaceId)
    let imageRotation = output.getPreviewRotation(0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getSupportedFrameRates()

```cangjie
public func getSupportedFrameRates(): Array<FrameRateRange>
```

**Function:** Queries the supported frame rate ranges.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[FrameRateRange](#class-frameraterange)> | List of supported frame rate ranges. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createPreviewOutput(ability.previewProfiles[0], surfaceId)
    let frameRateRanges = output.getSupportedFrameRates()
} catch (e: BusinessException) {
    Hilog.info(0, "0", "${e.message}")
}
```

### func off(CameraEvents, Callback0Argument)

```cangjie
public func off(eventType: CameraEvents, callback: Callback0Argument): Unit
```

**Function:** Unregisters the listener for a specific event.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for. Must be one of [FrameStart, FrameEnd, CameraError]; otherwise, a 401 parameter error will be thrown. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | The callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(设备, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createPreviewOutput(ability.previewProfiles[0], surfaceId)
    output.off(CameraEvents.CameraError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents)

```cangjie
public func off(eventType: CameraEvents): Unit
```

**Function:** Cancels all callbacks for the specified event.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for. Must be an event that can be listened to via the `on` function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createPreviewOutput(ability.previewProfiles[0], surfaceId)
    output.off(CameraEvents.CameraError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback0Argument)

```cangjie
public func on(eventType: CameraEvents, callback: Callback0Argument): Unit
```

**Function:** Listens for the start of preview frames and obtains results via registered callback functions. Uses asynchronous callback.

> **Note:**
>
> Calling `off` to unregister callbacks within the callback method of `on` is not supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | The event to listen for. Must be one of [FrameStart, FrameEnd, CameraError]; otherwise, a 401 parameter error will be thrown. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | The callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.callback_invoke.Callback0Argument
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class TestCallbackError <: Callback0Argument {
        public init() {}
        public open func invoke(res: ?BusinessException): Unit {
            Hilog.info(0, "Camera", "Call invoke error. code: ${res?.code}, msg: ${res?.message}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createPreviewOutput(ability.previewProfiles[0], surfaceId)
    let testCallbackError = TestCallbackError()
    output.on(CameraEvents.CameraError, testCallbackError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func release()

```cangjie
public func release(): Unit
```

**Function:** Releases output resources.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[0]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output =## class Profile

```cangjie
public open class Profile {
    public let format: CameraFormat
    public let size: Size
}
```

**Description:** Camera configuration information item.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let format

```cangjie
public let format: CameraFormat
```

**Description:** Output format.

**Type:** [CameraFormat](#enum-cameraformat)

**Accessibility:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let size

```cangjie
public let size: Size
```

**Description:** Resolution. Sets the camera resolution width and height, not the actual output image dimensions.

**Type:** [Size](#class-size)

**Accessibility:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class Rect

```cangjie
public class Rect {
    public var topLeftX: Float64
    public var topLeftY: Float64
    public var width: Float64
    public var height: Float64
}
```

**Description:** Rectangle definition.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var height

```cangjie
public var height: Float64
```

**Description:** Rectangle height, relative value, range [0.0, 1.0].

**Type:** Float64

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var topLeftX

```cangjie
public var topLeftX: Float64
```

**Description:** X-coordinate of the top-left corner of the rectangle area.

**Type:** Float64

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var topLeftY

```cangjie
public var topLeftY: Float64
```

**Description:** Y-coordinate of the top-left corner of the rectangle area.

**Type:** Float64

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var width

```cangjie
public var width: Float64
```

**Description:** Rectangle width, relative value, range [0.0, 1.0].

**Type:** Float64

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class Size

```cangjie
public class Size {
    public var width: UInt32
    public var height: UInt32
}
```

**Description:** Output capability query.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var height

```cangjie
public var height: UInt32
```

**Description:** Image height (in pixels).

**Type:** UInt32

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var width

```cangjie
public var width: UInt32
```

**Description:** Image width (in pixels).

**Type:** UInt32

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class SmoothZoomInfo

```cangjie
public class SmoothZoomInfo {
    public var duration: Int32
}
```

**Description:** Smooth zoom parameter information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### var duration

```cangjie
public var duration: Int32
```

**Description:** Total duration of smooth zoom, in milliseconds.

**Type:** Int32

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class TorchStatusInfo

```cangjie
public class TorchStatusInfo {
    public let isTorchAvailable: Bool
    public let isTorchActive: Bool
    public let torchLevel: Float64
}
```

**Description:** Interface instance returned by the torch callback, representing torch status information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let isTorchActive

```cangjie
public let isTorchActive: Bool
```

**Description:** Whether the torch is activated.

**Type:** Bool

**Accessibility:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let isTorchAvailable

```cangjie
public let isTorchAvailable: Bool
```

**Description:** Whether the torch is available.

**Type:** Bool

**Accessibility:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### let torchLevel

```cangjie
public let torchLevel: Float64
```

**Description:** Torch brightness level. Range [0.0, 1.0], where values closer to 1 indicate higher brightness.

**Type:** Float64

**Accessibility:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class VideoOutput

```cangjie
public class VideoOutput  <:  CameraOutput {}
```

**Description:** Output information used in video recording sessions.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Type:**

- [CameraOutput](#interface-cameraoutput)

### func getActiveFrameRate()

```cangjie
public func getActiveFrameRate(): FrameRateRange
```

**Description:** Gets the set frame rate range. Can be queried after setting the frame rate for the video stream using setFrameRate.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[FrameRateRange](#class-frameraterange)|Frame rate range.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[1]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createVideoOutput(ability.videoProfiles[0], surfaceId)
    let frameRateRange = output.getActiveFrameRate()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getActiveProfile()

```cangjie
public func getActiveProfile(): VideoProfile
```

**Description:** Gets the currently active configuration information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[VideoProfile](#class-videoprofile)|Currently active configuration information.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[1]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createVideoOutput(ability.videoProfiles[0], surfaceId)
    let videoProfile = output.getActiveProfile()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getSupportedFrameRates()

```cangjie
public func getSupportedFrameRates(): Array<FrameRateRange>
```

**Description:** Queries the supported frame rate ranges.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Array\<[FrameRateRange](#class-frameraterange)>|List of supported frame rate ranges.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[1]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createVideoOutput(ability.videoProfiles[0], surfaceId)
    let frameRateRanges = output.getSupportedFrameRates()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func getVideoRotation(Int32)

```cangjie
public func getVideoRotation(deviceDegree: Int32): ImageRotation
```

**Function:** Get video recording rotation angle.

- **Device Natural Orientation:** The default orientation of the device, typically portrait mode for smartphones (charging port facing downward).
- **Camera Lens Angle:** The value equals the clockwise rotation angle required to align the camera image with the device's natural orientation. For smartphone rear cameras, the sensor is mounted vertically, thus requiring a 90-degree clockwise rotation to match the device's natural orientation.
- **Screen Display Direction:** The displayed image should have its top-left corner as the coordinate origin (first pixel point). When the screen is locked, this aligns with the natural orientation.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| deviceDegree | Int32 | Yes | - | Device rotation angle. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ImageRotation](#enum-imagerotation) | Video recording rotation angle. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[1]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createVideoOutput(ability.videoProfiles[0], surfaceId)
    let imageRotation = output.getVideoRotation(0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback0Argument)

```cangjie
public func off(eventType: CameraEvents, callback: Callback0Argument): Unit
```

**Function:** Unregister a specific callback function for a specific event.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Event to unregister, must be one of [FrameStart, FrameEnd, CameraError]. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function to remove. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[1]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createVideoOutput(ability.videoProfiles[0], surfaceId)
    output.off(CameraEvents.CameraError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents)

```cangjie
public func off(eventType: CameraEvents): Unit
```

**Function:** Remove all callbacks for the specified event.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Event to unregister, must be one of [FrameStart, FrameEnd, CameraError]. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[1]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createVideoOutput(ability.videoProfiles[0], surfaceId)
    output.off(CameraEvents.CameraError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback0Argument)

```cangjie
public func on(eventType: CameraEvents, callback: Callback0Argument): Unit
```

**Function:** Listen for specific events during video recording.

> **Note:**
>
> Calling `off` to unregister callbacks within an `on` callback is not supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Event to listen for, must be one of [FrameStart, FrameEnd, CameraError]. Can be listened to after `videoOutput` is successfully created. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function. Captures no information during normal operation but captures error information when an error occurs. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.callback_invoke.Callback0Argument
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    //// check redundant import

    //// end

    // This code can be added to dependency definitions
    class TestCallbackError <: Callback0Argument {
        public init() {}
        public open func invoke(res: ?BusinessException): Unit {
            Hilog.info(0, "Camera", "Call invoke error. code: ${res?.code}, msg: ${res?.message}")
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[1]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createVideoOutput(ability.videoProfiles[0], surfaceId)
    let testCallbackError = TestCallbackError()
    output.on(CameraEvents.CameraError, testCallbackError)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func release()

```cangjie
public func release(): Unit
```

**Function:** Release output resources.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since Version:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[1]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createVideoOutput(ability.videoProfiles[0], surfaceId)
    output.release()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setFrameRate(Int32, Int32)

```cangjie
public func setFrameRate(minFps: Int32, maxFps: Int32): Unit
```

**Function:** Set the frame rate range for video recording. The specified range must be within the supported frame rate range. Before setting, query supported ranges via [getSupportedFrameRates](#func-getsupportedframerates).

> **Note:**
>
> Only supported in [PhotoSession](#class-photosession) or [VideoSession](#class-videosession) modes.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| minFps | Int32 | Yes | - | Minimum frame rate. |
| maxFps | Int32 | Yes | - | Maximum frame rate. If the minimum value exceeds the maximum, the parameters are invalid, and the interface will not take effect. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400101 | Parameter missing or parameter type incorrect. |
  | 7400110 | Unresolved conflicts with current configurations. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[1]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createVideoOutput(ability.videoProfiles[0], surfaceId)
    output.setFrameRate(30, 60)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func start()

```cangjie
public func start(): Unit
```

**Function:** Start recording.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since Version:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400103 | Session not config. |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[1]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createVideoOutput(ability.videoProfiles[0], surfaceId)
    output.start()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func stop()

```cangjie
public func stop(): Unit
```

**Function:** Stop recording.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since Version:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.ImageKit.createImageReceiver
import kit.ImageKit.Size as ImageSize
import kit.ImageKit.ImageFormat
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let device = cameraManager.getSupportedCameras()[0]
    let mode = cameraManager.getSupportedSceneModes(device)[1]
    let ability = cameraManager.getSupportedOutputCapability(device, mode)
    let size = ImageSize(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let surfaceId: String = receiver.getReceivingSurfaceId()
    let output = cameraManager.createVideoOutput(ability.videoProfiles[0], surfaceId)
    output.stop()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class VideoProfile

```cangjie
public class VideoProfile <: Profile {
    public let frameRateRange: FrameRateRange
}
```

**Function:** Video configuration item.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Type:**

- [Profile](#class-profile)

### let frameRateRange

```cangjie
public let frameRateRange: FrameRateRange
```

**Function:** Frame rate range, fps (frames per second).

**Type:** [FrameRateRange](#class-frameraterange)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

## class VideoSession

```cangjie
public class VideoSession  Session & Flash & AutoExposure & Focus & Zoom & Stabilization & ColorManagement {}
```

**Function:** A session class for normal video recording mode, providing operations for flash, exposure, focus, zoom, video stabilization, and color space.

> **Note:**
>
> The default video recording mode, suitable for general scenarios. Supports recording at various resolutions such as 720P and 1080p, with selectable frame rates (e.g., 30fps, 60fps).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- [Session](#interface-session)
- [Flash](#interface-flash)
- [AutoExposure](#interface-autoexposure)
- [Focus](#interface-focus)
- [Zoom](#interface-zoom)
- [Stabilization](#interface-stabilization)
- [ColorManagement](#interface-colormanagement)

### func canPreconfig(PreconfigType, PreconfigRatio)

```cangjie
public func canPreconfig(preconfigType: PreconfigType, preconfigRatio!: PreconfigRatio = PreconfigRatio_16_9): Bool
```

**Function:** Queries whether the current Session supports the specified preconfiguration type.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| preconfigType | [PreconfigType](#enum-preconfigtype) | Yes | - | Specifies the expected resolution for configuration. |
| preconfigRatio | [PreconfigRatio](#enum-preconfigratio) | No | PreconfigRatio_16_9 | **Named parameter.** Optional aspect ratio. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: Supports the specified preconfiguration type. false: Does not support the specified preconfiguration type. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let videoSession = cameraManager.createSession(SceneMode.NormalVideo) as VideoSession
    let session = videoSession.getOrThrow()
    session.canPreconfig(Preconfig1080p, preconfigRatio: PreconfigRatio_16_9)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback0Argument)

```cangjie
public func off(eventType: CameraEvents, callback: Callback0Argument): Unit
```

**Function:** Unregisters the listener for error events in normal video recording sessions.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be CameraError. This interface can be listened to after the session is successfully created. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function to cancel the corresponding callback. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let videoSession = cameraManager.createSession(SceneMode.NormalVideo) as VideoSession
    let session = videoSession.getOrThrow()
    session.off(CameraEvents.SmoothZoomInfoAvailable)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback1Argument\<FocusState>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<FocusState>): Unit
```

**Function:** Unregisters the listener for focus state changes in normal video recording sessions.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be FocusStateChange. This interface can be listened to after the session is successfully created. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[FocusState](#enum-focusstate)> | Yes | - | Callback function to cancel the corresponding callback. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let videoSession = cameraManager.createSession(SceneMode.NormalVideo) as VideoSession
    let session = videoSession.getOrThrow()
    session.off(CameraEvents.SmoothZoomInfoAvailable)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents, Callback1Argument\<SmoothZoomInfo>)

```cangjie
public func off(eventType: CameraEvents, callback: Callback1Argument<SmoothZoomInfo>): Unit
```

**Function:** Unregisters the listener for smooth zoom state changes in normal video recording sessions.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be SmoothZoomInfoAvailable. This interface can be listened to after the session is successfully created. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[SmoothZoomInfo](#class-smoothzoominfo)> | Yes | - | Callback function to cancel the corresponding callback. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let videoSession = cameraManager.createSession(SceneMode.NormalVideo) as VideoSession
    let session = videoSession.getOrThrow()
    session.off(CameraEvents.SmoothZoomInfoAvailable)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(CameraEvents)

```cangjie
public func off(eventType: CameraEvents): Unit
```

**Function:** Unregisters the listener for error events in normal video recording sessions.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let videoSession = cameraManager.createSession(SceneMode.NormalVideo) as VideoSession
    let session = videoSession.getOrThrow()
    session.off(CameraEvents.SmoothZoomInfoAvailable)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback0Argument)

```cangjie
public func on(eventType: CameraEvents, callback: Callback0Argument): Unit
```

**Function:** Listens for error events in normal video recording sessions and obtains results through registered callback functions.

> **Note:**
>
> Calling `off` to unregister callbacks within the callback method of `on` is not supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be CameraError. This interface can be listened to after the session is successfully created. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function to obtain error information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.*
import ohos.business_exception.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class SmoothZoomInfoAvailableCallback <: Callback1Argument<SmoothZoomInfo> {
        public static var invoked = false

        public func invoke(err: ?BusinessException, info: SmoothZoomInfo) {
            Hilog.info(0, "AppLogCj", "[multimedia_camera | SmoothZoomInfoAvailable Callback]: info: ${info.duration}")

            invoked = true
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let videoSession = cameraManager.createSession(SceneMode.NormalVideo) as VideoSession
    let session = videoSession.getOrThrow()
    let callback = SmoothZoomInfoAvailableCallback()
    session.on(CameraEvents.SmoothZoomInfoAvailable, callback)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback1Argument\<FocusState>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<FocusState>): Unit
```

**Function:** Listens for focus state changes in normal video recording sessions and obtains results through registered callback functions.

> **Note:**
>
> Calling `off` to unregister callbacks within the callback method of `on` is not supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be FocusStateChange. This interface can be listened to after the session is successfully created. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[FocusState](#enum-focusstate)> | Yes | - | Callback function to obtain focus state change information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.*
import ohos.business_exception.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class SmoothZoomInfoAvailableCallback <: Callback1Argument<SmoothZoomInfo> {
        public static var invoked = false

        public func invoke(err: ?BusinessException, info: SmoothZoomInfo) {
            Hilog.info(0, "AppLogCj", "[multimedia_camera | SmoothZoomInfoAvailable Callback]: info: ${info.duration}")

            invoked = true
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let videoSession = cameraManager.createSession(SceneMode.NormalVideo) as VideoSession
    let session = videoSession.getOrThrow()
    let callback = SmoothZoomInfoAvailableCallback()
    session.on(CameraEvents.SmoothZoomInfoAvailable, callback)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(CameraEvents, Callback1Argument\<SmoothZoomInfo>)

```cangjie
public func on(eventType: CameraEvents, callback: Callback1Argument<SmoothZoomInfo>): Unit
```

**Function:** Listens for smooth zoom state changes in normal video recording sessions and obtains results through registered callback functions.

> **Note:**
>
> Calling `off` to unregister callbacks within the callback method of `on` is not supported.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [CameraEvents](#enum-cameraevents) | Yes | - | Listening event, must be SmoothZoomInfoAvailable. This interface can be listened to after the session is successfully created. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[SmoothZoomInfo](#class-smoothzoominfo)> | Yes | - | Callback function to obtain smooth zoom state change information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 7400201 | Camera service fatal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import ohos.callback_invoke.*
import ohos.business_exception.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class SmoothZoomInfoAvailableCallback <: Callback1Argument<SmoothZoomInfo> {
        public static var invoked = false

        public func invoke(err: ?BusinessException, info: SmoothZoomInfo) {
            Hilog.info(0, "AppLogCj", "[multimedia_camera | SmoothZoomInfoAvailable Callback]: info: ${info.duration}")

            invoked = true
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let cameraManager = getCameraManager(ctx)
    let videoSession = cameraManager.createSession(SceneMode.NormalVideo) as VideoSession
    let session = videoSession.getOrThrow()
    let callback = SmoothZoomInfoAvailableCallback()
    session.on(CameraEvents.SmoothZoomInfoAvailable, callback)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func preconfig(PreconfigType, PreconfigRatio)

```cangjie
public func## enum CameraEvents

```cangjie
public enum CameraEvents {
    | CameraError
    | CameraStatus
    | FoldStatusChange
    | TorchStatusChange
    | FrameStart
    | FrameEnd
    | CaptureStartWithInfo
    | FrameShutter
    | CaptureEnd
    | FrameShutterEnd
    | CaptureReady
    | EstimatedCaptureDuration
    | MetadataObjectsAvailable
    | FocusStateChange
    | SmoothZoomInfoAvailable
    | ...
}
```

**Function:** Event names for monitoring.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Type:**

- Equatable\<CameraEvents>

### CameraError

```cangjie
CameraError
```

**Function:** Error event.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraStatus

```cangjie
CameraStatus
```

**Function:** Camera status change.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CaptureEnd

```cangjie
CaptureEnd
```

**Function:** Photo capture completion.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CaptureReady

```cangjie
CaptureReady
```

**Function:** Ready for next capture.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CaptureStartWithInfo

```cangjie
CaptureStartWithInfo
```

**Function:** Photo capture initiation.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### EstimatedCaptureDuration

```cangjie
EstimatedCaptureDuration
```

**Function:** Estimated capture duration.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FocusStateChange

```cangjie
FocusStateChange
```

**Function:** Camera focus state change.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FoldStatusChange

```cangjie
FoldStatusChange
```

**Function:** Foldable device fold status change.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FrameEnd

```cangjie
FrameEnd
```

**Function:** Preview frame completion.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FrameShutter

```cangjie
FrameShutter
```

**Function:** Capture frame output.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FrameShutterEnd

```cangjie
FrameShutterEnd
```

**Function:** Photo exposure completion.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FrameStart

```cangjie
FrameStart
```

**Function:** Preview frame initiation.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### MetadataObjectsAvailable

```cangjie
MetadataObjectsAvailable
```

**Function:** Metadata objects detected.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### SmoothZoomInfoAvailable

```cangjie
SmoothZoomInfoAvailable
```

**Function:** Camera smooth zoom state change.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### TorchStatusChange

```cangjie
TorchStatusChange
```

**Function:** Flashlight status change.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(CameraEvents)

```cangjie
public operator func !=(other: CameraEvents): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Mandatory|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CameraEvents](#enum-cameraevents)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|true indicates equal, false indicates unequal.|

### func ==(CameraEvents)

```cangjie
public operator func ==(other: CameraEvents): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Mandatory|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CameraEvents](#enum-cameraevents)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|true indicates unequal, false indicates equal.|

## enum CameraFormat

```cangjie
public enum CameraFormat {
    | CameraFormatYcbcrP010
    | CameraFormatYcrcbP010
    | CameraFormatHeic
    | CameraFormatJpeg
    | CameraFormatYuv420Sp
    | CameraFormatRgba8888
    | ...
}
```

**Function:** Output formats.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<CameraFormat>
- ToString

### CameraFormatHeic

```cangjie
CameraFormatHeic
```

**Function:** HEIF format image.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraFormatJpeg

```cangjie
CameraFormatJpeg
```

**Function:** JPEG format image.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraFormatRgba8888

```cangjie
CameraFormatRgba8888
```

**Function:** RGBA_8888 format image.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraFormatYcbcrP010

```cangjie
CameraFormatYcbcrP010
```

**Function:** YCBCR_P010 format image.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraFormatYcrcbP010

```cangjie
CameraFormatYcrcbP010
```

**Function:** YCRCB_P010 format image.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraFormatYuv420Sp

```cangjie
CameraFormatYuv420Sp
```

**Function:** YUV_420_SP format image.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(CameraFormat)

```cangjie
public operator func !=(other: CameraFormat): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Mandatory|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CameraFormat](#enum-cameraformat)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if unequal, otherwise false.|

### func ==(CameraFormat)

```cangjie
public operator func ==(other: CameraFormat): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Mandatory|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CameraFormat](#enum-cameraformat)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if unequal, otherwise false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|String value of the enum.|## enum CameraPosition

```cangjie
public enum CameraPosition {
    | CameraPositionUnspecified
    | CameraPositionBack
    | CameraPositionFront
    | ...
}
```

**Function:** Camera position.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<CameraPosition>
- ToString

### CameraPositionBack

```cangjie
CameraPositionBack
```

**Function:** Rear camera.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraPositionFront

```cangjie
CameraPositionFront
```

**Function:** Front camera.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraPositionUnspecified

```cangjie
CameraPositionUnspecified
```

**Function:** Camera position unspecified.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(CameraPosition)

```cangjie
public operator func !=(other: CameraPosition): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CameraPosition](#enum-cameraposition)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(CameraPosition)

```cangjie
public operator func ==(other: CameraPosition): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CameraPosition](#enum-cameraposition)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string value of the enum.|

## enum CameraStatus

```cangjie
public enum CameraStatus {
    | CameraStatusAppear
    | CameraStatusDisappear
    | CameraStatusAvailable
    | CameraStatusUnavailable
    | ...
}
```

**Function:** Camera status.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<CameraStatus>
- ToString

### CameraStatusAppear

```cangjie
CameraStatusAppear
```

**Function:** New camera appears.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraStatusAvailable

```cangjie
CameraStatusAvailable
```

**Function:** Camera is available.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraStatusDisappear

```cangjie
CameraStatusDisappear
```

**Function:** Camera is removed.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraStatusUnavailable

```cangjie
CameraStatusUnavailable
```

**Function:** Camera is unavailable.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(CameraStatus)

```cangjie
public operator func !=(other: CameraStatus): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CameraStatus](#enum-camerastatus)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(CameraStatus)

```cangjie
public operator func ==(other: CameraStatus): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CameraStatus](#enum-camerastatus)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string value of the enum.|

## enum CameraType

```cangjie
public enum CameraType {
    | CameraTypeDefault
    | CameraTypeWideAngle
    | CameraTypeUltraWide
    | CameraTypeTelephoto
    | CameraTypeTrueDepth
    | ...
}
```

**Function:** Camera type.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<CameraType>
- ToString

### CameraTypeDefault

```cangjie
CameraTypeDefault
```

**Function:** Camera type unspecified.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraTypeTelephoto

```cangjie
CameraTypeTelephoto
```

**Function:** Telephoto camera.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraTypeTrueDepth

```cangjie
CameraTypeTrueDepth
```

**Function:** Camera with depth information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraTypeUltraWide

```cangjie
CameraTypeUltraWide
```

**Function:** Ultra-wide camera.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraTypeWideAngle

```cangjie
CameraTypeWideAngle
```

**Function:** Wide-angle camera.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(CameraType)

```cangjie
public operator func !=(other: CameraType): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CameraType](#enum-cameratype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(CameraType)

```cangjie
public operator func ==(other: CameraType): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CameraType](#enum-cameratype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string value of the enum.|

## enum ConnectionType

```cangjie
public enum ConnectionType {
    | CameraConnectionBuiltIn
    | CameraConnectionUsbPlugin
    | CameraConnectionRemote
    | ...
}
```

**Function:** Camera connection type.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<ConnectionType>
- ToString

### CameraConnectionBuiltIn

```cangjie
CameraConnectionBuiltIn
```

**Function:** Built-in camera.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraConnectionRemote

```cangjie
CameraConnectionRemote
```

**Function:** Remotely connected camera.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### CameraConnectionUsbPlugin

```cangjie
CameraConnectionUsbPlugin
```

**Function:** USB-connected camera.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(ConnectionType)

```cangjie
public operator func !=(other: ConnectionType): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ConnectionType](#enum-connectiontype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(ConnectionType)

```cangjie
public operator func ==(other: ConnectionType): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ConnectionType](#enum-connectiontype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string value of the enum.|```markdown
## enum ExposureMode

```cangjie
public enum ExposureMode {
    | ExposureModeLocked
    | ExposureModeAuto
    | ExposureModeContinuousAuto
    | ...
}
```

**Description:** Exposure mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<ExposureMode>
- ToString

### ExposureModeAuto

```cangjie
ExposureModeAuto
```

**Description:** Auto exposure mode. Supports setting the center point of the exposure area via [AutoExposure.setMeteringPoint](#func-setmeteringpointpoint).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### ExposureModeContinuousAuto

```cangjie
ExposureModeContinuousAuto
```

**Description:** Continuous auto exposure. Does not support setting the center point of the exposure area.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### ExposureModeLocked

```cangjie
ExposureModeLocked
```

**Description:** Locked exposure mode. Does not support setting the center point of the exposure area.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(ExposureMode)

```cangjie
public operator func !=(other: ExposureMode): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ExposureMode](#enum-exposuremode) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are unequal, otherwise false. |

### func ==(ExposureMode)

```cangjie
public operator func ==(other: ExposureMode): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ExposureMode](#enum-exposuremode) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are equal, otherwise false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the string value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string value of the enum. |

## enum FlashMode

```cangjie
public enum FlashMode {
    | FlashModeClose
    | FlashModeOpen
    | FlashModeAuto
    | FlashModeAlwaysOpen
    | ...
}
```

**Description:** Flash mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<FlashMode>
- ToString

### FlashModeAlwaysOpen

```cangjie
FlashModeAlwaysOpen
```

**Description:** Flash always on.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FlashModeAuto

```cangjie
FlashModeAuto
```

**Description:** Auto flash.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FlashModeClose

```cangjie
FlashModeClose
```

**Description:** Flash off.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FlashModeOpen

```cangjie
FlashModeOpen
```

**Description:** Flash on.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(FlashMode)

```cangjie
public operator func !=(other: FlashMode): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FlashMode](#enum-flashmode) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are unequal, otherwise false. |

### func ==(FlashMode)

```cangjie
public operator func ==(other: FlashMode): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FlashMode](#enum-flashmode) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are equal, otherwise false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the string value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string value of the enum. |

## enum FocusMode

```cangjie
public enum FocusMode {
    | FocusModeManual
    | FocusModeContinuousAuto
    | FocusModeAuto
    | FocusModeLocked
    | ...
}
```

**Description:** Focus mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<FocusMode>
- ToString

### FocusModeAuto

```cangjie
FocusModeAuto
```

**Description:** Auto focus. Supports focus point setting via [setFocusPoint](#func-setfocuspointpoint), performing auto focus once based on the focus point.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FocusModeContinuousAuto

```cangjie
FocusModeContinuousAuto
```

**Description:** Continuous auto focus. Does not support focus point setting.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FocusModeLocked

```cangjie
FocusModeLocked
```

**Description:** Focus locked. Does not support focus point setting.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FocusModeManual

```cangjie
FocusModeManual
```

**Description:** Manual focus. Adjusts focus position by manually modifying the camera's focal length. Does not support focus point setting.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(FocusMode)

```cangjie
public operator func !=(other: FocusMode): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FocusMode](#enum-focusmode) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are unequal, otherwise false. |

### func ==(FocusMode)

```cangjie
public operator func ==(other: FocusMode): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FocusMode](#enum-focusmode) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are equal, otherwise false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the string value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string value of the enum. |

## enum FocusState

```cangjie
public enum FocusState {
    | FocusStateScan
    | FocusStateFocused
    | FocusStateUnfocused
    | ...
}
```

**Description:** Focus state.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<FocusState>
- ToString

### FocusStateFocused

```cangjie
FocusStateFocused
```

**Description:** Focus succeeded.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FocusStateScan

```cangjie
FocusStateScan
```

**Description:** Focus triggered.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### FocusStateUnfocused

```cangjie
FocusStateUnfocused
```

**Description:** Focus not completed.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(FocusState)

```cangjie
public operator func !=(other: FocusState): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FocusState](#enum-focusstate) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are unequal, otherwise false. |

### func ==(FocusState)

```cangjie
public operator func ==(other: FocusState): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FocusState](#enum-focusstate) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are equal, otherwise false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the string value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string value of the enum. |
```## enum FoldStatus

```cangjie
public enum FoldStatus {
    | NonFoldable
    | Expanded
    | Folded
    | ...
}
```

**Description:** Folding state of foldable devices.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<FoldStatus>
- ToString

### Expanded

```cangjie
Expanded
```

**Description:** Indicates the device is in fully unfolded state.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### Folded

```cangjie
Folded
```

**Description:** Indicates the device is in folded state.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### NonFoldable

```cangjie
NonFoldable
```

**Description:** Indicates the device is non-foldable.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(FoldStatus)

```cangjie
public operator func !=(other: FoldStatus): Bool
```

**Description:** Checks whether two enum values are unequal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[FoldStatus](#enum-foldstatus)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are unequal, otherwise returns false.|

### func ==(FoldStatus)

```cangjie
public operator func ==(other: FoldStatus): Bool
```

**Description:** Checks whether two enum values are equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[FoldStatus](#enum-foldstatus)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the string representation of the enum value.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the enum value.|

## enum ImageRotation

```cangjie
public enum ImageRotation {
    | Rotation0
    | Rotation90
    | Rotation180
    | Rotation270
    | ...
}
```

**Description:** Image rotation angles.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<ImageRotation>
- ToString

### Rotation0

```cangjie
Rotation0
```

**Description:** 0-degree image rotation.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### Rotation180

```cangjie
Rotation180
```

**Description:** 180-degree image rotation.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### Rotation270

```cangjie
Rotation270
```

**Description:** 270-degree image rotation.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### Rotation90

```cangjie
Rotation90
```

**Description:** 90-degree image rotation.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(ImageRotation)

```cangjie
public operator func !=(other: ImageRotation): Bool
```

**Description:** Checks whether two enum values are unequal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ImageRotation](#enum-imagerotation)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are unequal, otherwise returns false.|

### func ==(ImageRotation)

```cangjie
public operator func ==(other: ImageRotation): Bool
```

**Description:** Checks whether two enum values are equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ImageRotation](#enum-imagerotation)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the string representation of the enum value.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the enum value.|

## enum MetadataObjectType

```cangjie
public enum MetadataObjectType {
    | FaceDetection
    | ...
}
```

**Description:** Metadata stream.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<MetadataObjectType>
- ToString

### FaceDetection

```cangjie
FaceDetection
```

**Description:** Metadata object type for face detection. Detection points should be in the 0-1 coordinate system where the top-left corner is (0.0, 0.0) and the bottom-right corner is (1.0, 1.0). This coordinate system is based on the landscape device orientation with the charging port on the right. For example, if the application's preview layout is based on portrait orientation with the charging port at the bottom, and the layout dimensions are (w, h), with returned points (x, y), the converted coordinates would be (1.0-y, x).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(MetadataObjectType)

```cangjie
public operator func !=(other: MetadataObjectType): Bool
```

**Description:** Checks whether two enum values are unequal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[MetadataObjectType](#enum-metadataobjecttype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are unequal, otherwise returns false.|

### func ==(MetadataObjectType)

```cangjie
public operator func ==(other: MetadataObjectType): Bool
```

**Description:** Checks whether two enum values are equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[MetadataObjectType](#enum-metadataobjecttype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the string representation of the enum value.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the enum value.|

## enum PreconfigRatio

```cangjie
public enum PreconfigRatio {
    | PreconfigRatio_1_1
    | PreconfigRatio_4_3
    | PreconfigRatio_16_9
    | ...
}
```

**Description:** Provides preconfigured resolution ratios.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<PreconfigRatio>
- ToString

### PreconfigRatio_16_9

```cangjie
PreconfigRatio_16_9
```

**Description:** 16:9 aspect ratio.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### PreconfigRatio_1_1

```cangjie
PreconfigRatio_1_1
```

**Description:** 1:1 aspect ratio.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### PreconfigRatio_4_3

```cangjie
PreconfigRatio_4_3
```

**Description:** 4:3 aspect ratio.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(PreconfigRatio)

```cangjie
public operator func !=(other: PreconfigRatio): Bool
```

**Description:** Checks whether two enum values are unequal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[PreconfigRatio](#enum-preconfigratio)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are unequal, otherwise returns false.|

### func ==(PreconfigRatio)

```cangjie
public operator func ==(other: PreconfigRatio): Bool
```

**Description:** Checks whether two enum values are equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[PreconfigRatio](#enum-preconfigratio)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the string representation of the enum value.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the enum value.|## enum PreconfigType

```cangjie
public enum PreconfigType {
    | Preconfig720p
    | Preconfig1080p
    | Preconfig4k
    | PreconfigHighQuality
    | ...
}
```

**Function:** Provides preconfigured types.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<PreconfigType>
- ToString

### Preconfig1080p

```cangjie
Preconfig1080p
```

**Function:** 1080P preconfiguration.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### Preconfig4k

```cangjie
Preconfig4k
```

**Function:** 4K preconfiguration.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### Preconfig720p

```cangjie
Preconfig720p
```

**Function:** 720P preconfiguration.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### PreconfigHighQuality

```cangjie
PreconfigHighQuality
```

**Function:** High-quality preconfiguration.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(PreconfigType)

```cangjie
public operator func !=(other: PreconfigType): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[PreconfigType](#enum-preconfigtype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(PreconfigType)

```cangjie
public operator func ==(other: PreconfigType): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[PreconfigType](#enum-preconfigtype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string value of the enum.|

## enum QualityLevel

```cangjie
public enum QualityLevel {
    | QualityLevelHigh
    | QualityLevelMedium
    | QualityLevelLow
    | ...
}
```

**Function:** Image quality.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<QualityLevel>
- ToString

### QualityLevelHigh

```cangjie
QualityLevelHigh
```

**Function:** High image quality.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### QualityLevelLow

```cangjie
QualityLevelLow
```

**Function:** Low image quality.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### QualityLevelMedium

```cangjie
QualityLevelMedium
```

**Function:** Medium image quality.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(QualityLevel)

```cangjie
public operator func !=(other: QualityLevel): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[QualityLevel](#enum-qualitylevel)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(QualityLevel)

```cangjie
public operator func ==(other: QualityLevel): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[QualityLevel](#enum-qualitylevel)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string value of the enum.|

## enum SceneMode

```cangjie
public enum SceneMode {
    | NormalPhoto
    | NormalVideo
    | SecurePhoto
    | ...
}
```

**Function:** Camera-supported modes.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<SceneMode>
- ToString

### NormalPhoto

```cangjie
NormalPhoto
```

**Function:** Normal photo mode. For details, see [PhotoSession](#class-photosession).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### NormalVideo

```cangjie
NormalVideo
```

**Function:** Normal video mode. For details, see [VideoSession](#class-videosession).

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### SecurePhoto

```cangjie
SecurePhoto
```

**Function:** Secure camera mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(SceneMode)

```cangjie
public operator func !=(other: SceneMode): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SceneMode](#enum-scenemode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(SceneMode)

```cangjie
public operator func ==(other: SceneMode): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SceneMode](#enum-scenemode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string value of the enum.|

## enum SmoothZoomMode

```cangjie
public enum SmoothZoomMode {
    | Normal
    | ...
}
```

**Function:** Smooth zoom mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<SmoothZoomMode>
- ToString

### Normal

```cangjie
Normal
```

**Function:** Bezier curve mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(SmoothZoomMode)

```cangjie
public operator func !=(other: SmoothZoomMode): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SmoothZoomMode](#enum-smoothzoommode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(SmoothZoomMode)

```cangjie
public operator func ==(other: SmoothZoomMode): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SmoothZoomMode](#enum-smoothzoommode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string value of the enum.|## enum TorchMode

```cangjie
public enum TorchMode {
    | Off
    | On
    | Auto
    | ...
}
```

**Function:** Flashlight mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<TorchMode>
- ToString

### Auto

```cangjie
Auto
```

**Function:** Automatic mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### Off

```cangjie
Off
```

**Function:** Always-off mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### On

```cangjie
On
```

**Function:** Always-on mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(TorchMode)

```cangjie
public operator func !=(other: TorchMode): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[TorchMode](#enum-torchmode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(TorchMode)

```cangjie
public operator func ==(other: TorchMode): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[TorchMode](#enum-torchmode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string value of the enum.|

## enum VideoCodecType

```cangjie
public enum VideoCodecType {
    | Avc
    | Hevc
    | ...
}
```

**Function:** Video encoding type.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<VideoCodecType>
- ToString

### Avc

```cangjie
Avc
```

**Function:** Video encoding type AVC.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### Hevc

```cangjie
Hevc
```

**Function:** Video encoding type HEVC.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(VideoCodecType)

```cangjie
public operator func !=(other: VideoCodecType): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[VideoCodecType](#enum-videocodectype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(VideoCodecType)

```cangjie
public operator func ==(other: VideoCodecType): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[VideoCodecType](#enum-videocodectype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string value of the enum.|

## enum VideoStabilizationMode

```cangjie
public enum VideoStabilizationMode {
    | Off
    | Low
    | Middle
    | High
    | Auto
    | ...
}
```

**Function:** Video stabilization mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

**Parent Types:**

- Equatable\<VideoStabilizationMode>
- ToString

### Auto

```cangjie
Auto
```

**Function:** Automatic selection.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### High

```cangjie
High
```

**Function:** Uses the stabilization algorithm with the best effect, superior to MIDDLE type.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### Low

```cangjie
Low
```

**Function:** Disables video stabilization.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### Middle

```cangjie
Middle
```

**Function:** Uses a moderate stabilization algorithm, superior to LOW type.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### Off

```cangjie
Off
```

**Function:** Disables video stabilization.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 22

### func !=(VideoStabilizationMode)

```cangjie
public operator func !=(other: VideoStabilizationMode): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[VideoStabilizationMode](#enum-videostabilizationmode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(VideoStabilizationMode)

```cangjie
public operator func ==(other: VideoStabilizationMode): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[VideoStabilizationMode](#enum-videostabilizationmode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string value of the enum.

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string value of the enum.|