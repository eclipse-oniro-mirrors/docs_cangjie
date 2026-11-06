# 通过系统相机拍照和录像（CameraPicker）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

应用可调用CameraPicker拍摄照片或录制视频，无需申请相机权限。

CameraPicker的相机交互界面由系统提供，在用户点击拍摄和确认按钮后，调用CameraPicker的应用获取对应的照片或者视频。

应用开发者如果只是需要获取即时拍摄的照片或者视频，则可以使用CameraPicker能力来轻松实现。

由于照片的拍摄和确认都是由用户进行主动确认，因此应用开发者可以不用申请操作相机的相关权限。

## 开发步骤

详细的API说明请参见[ohos.multimedia.camera_picker（相机选择器）](../../reference/CameraKit/cj-apis-multimedia-camera-picker.md)。

1. 导入相关接口，导入方法如下。

    <!-- compile -->

    ```cangjie
    import kit.CameraKit.*
    import kit.CoreFileKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. 配置[PickerProfile](../../reference/CameraKit/cj-apis-multimedia-camera-picker.md#class-pickerprofile)。

    > **说明：**
    >
    > PickerProfile的saveUri为可选参数，如果未配置该项，拍摄的照片和视频默认存入媒体库中。
    >
    > 如果不想将照片和视频存入媒体库，请自行配置应用沙箱内的文件路径。
    > 应用沙箱内的这个文件必须是一个存在的、可写的文件。这个文件的uri传入pick接口之后，相当于应用给系统相机授权该文件的读写权限。系统相机在拍摄结束之后，会对此文件进行覆盖写入。

    <!-- compile -->

    ```cangjie
    func createPickerProfile(context: UIAbilityContext): PickerProfile {
        let pathDir = context.filesDir
        let filePath = pathDir + "/CameraPicker.tmp"
        let file = FileIo.open(filePath, mode: (OpenMode.READ_WRITE | OpenMode.CREATE))
        FileIo.close(file)
        let uri = getUriFromPath(filePath)

        let pickerProfile = PickerProfile(CameraPosition.CameraPositionBack, saveUri: Some(uri))
        return pickerProfile
    }
    ```

    FileIo接口调用方法请参考：[open](../../reference/CoreFileKit/cj-apis-file_fs.md#static-func-openstring-int64)和[getUriFromPath](../../reference/CoreFileKit/cj-apis-file_fileuri.md#func-geturifrompathstring)。

3. 调用[pick](../../reference/CameraKit/cj-apis-multimedia-camera-picker.md#func-pickuiabilitycontext-arraypickermediatype-pickerprofile-asynccallbackpickerresult)拍摄接口获取拍摄的结果。

    <!-- compile -->

    ```cangjie
    func getPickerResult(context: UIAbilityContext, pickerProfile: PickerProfile): Unit {
        let callback: AsyncCallback<PickerResult> = {
            err: Option<BusinessException>, data: Option<PickerResult> =>
            if (let Some(e) <- err) {
                Hilog.error(0, "test", "pick error: code=${e.code}, message=${e.message}")
            } else if (let Some(result) <- data) {
                Hilog.info(0, "test", "picker resultCode: ${result.resultCode}, resultUri: ${result.resultUri}, mediaType: ${result.mediaType}")
            }
        }
        pick(context, [PickerMediaType.Photo, PickerMediaType.Video], pickerProfile, callback)
    }
    ```

## 完整示例

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.CoreFileKit.*
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

func createPickerProfile(context: UIAbilityContext): PickerProfile {
    let pathDir = context.filesDir
    let filePath = pathDir + "/CameraPicker.tmp"
    let file = FileIo.open(filePath, mode: (OpenMode.READ_WRITE | OpenMode.CREATE))
    FileIo.close(file)
    let uri = getUriFromPath(filePath)

    let pickerProfile = PickerProfile(CameraPosition.CameraPositionBack, saveUri: Some(uri))
    return pickerProfile
}

func getPickerResult(context: UIAbilityContext, pickerProfile: PickerProfile): Unit {
    let callback: AsyncCallback<PickerResult> = {
        err: Option<BusinessException>, data: Option<PickerResult> =>
        if (let Some(e) <- err) {
            Hilog.error(0, "test", "pick error: code=${e.code}, message=${e.message}")
        } else if (let Some(result) <- data) {
            if (result.resultCode == 0) {
                match (result.mediaType) {
                    case PickerMediaType.Photo =>
                        Hilog.info(0, "test", "photo resultUri: ${result.resultUri}")
                    case PickerMediaType.Video =>
                        Hilog.info(0, "test", "video resultUri: ${result.resultUri}")
                    case _ =>
                        Hilog.info(0, "test", "unknown mediaType")
                }
            }
        }
    }
    pick(context, [PickerMediaType.Photo, PickerMediaType.Video], pickerProfile, callback)
}

// 此处需手动配置模板，获取Context上下文。上下文获取方式请参见使用说明。
let ctx = Global.abilityContext
let pickerProfile = createPickerProfile(ctx)
getPickerResult(ctx, pickerProfile)
```
