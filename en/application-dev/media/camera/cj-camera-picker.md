# Using the System Camera to Take Photos and Record Videos (CameraPicker)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The application can call CameraPicker to take photos or record videos without applying for the camera permission.

The camera interaction interface of CameraPicker is provided by the system. After the user taps the shooting and confirmation buttons, the application that calls CameraPicker obtains the corresponding photo or video.

If the application developer only needs to obtain instantly captured photos or videos, CameraPicker can be used to easily implement this.

Since photo shooting and confirmation are both actively performed by the user, the application developer does not need to apply for the permissions related to camera operations.

## How to Develop

For details about the APIs, see [ohos.multimedia.camera_picker (Camera Picker)](../../reference/CameraKit/cj-apis-multimedia-camera-picker.md).

1. Import the related modules as follows.

    <!-- compile -->

    ```cangjie
    import ohos.multimedia.camera_picker.*
    import kit.CameraKit.*
    import kit.CoreFileKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. Configure [PickerProfile](../../reference/CameraKit/cj-apis-multimedia-camera-picker.md#class-pickerprofile).

    > **Note:**
    >
    > **saveUri** of PickerProfile is an optional parameter. If it is not configured, the captured photos and videos are saved to the media library by default.
    >
    > If you do not want to save photos and videos to the media library, configure the file path in the application sandbox by yourself.
    > The file in the application sandbox must be an existing, writable file. After the URI of this file is passed to the pick API, the application authorizes the system camera to read and write the file. After the shooting is complete, the system camera overwrites this file.

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

    For details about how to call the FileIo APIs, see [open](../../reference/CoreFileKit/cj-apis-file_fs.md#static-func-openstring-int64) and [getUriFromPath](../../reference/CoreFileKit/cj-apis-file_fileuri.md#static-func-geturifrompathstring).

3. Call the [pick](../../reference/CameraKit/cj-apis-multimedia-camera-picker.md#func-pickuiabilitycontext-arraypickermediatype-pickerprofile-asynccallbackpickerresult) API to obtain the shooting result.

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

## Complete Example

<!-- compile -->

```cangjie
// index.cj

import ohos.multimedia.camera_picker.*
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

// The template must be configured manually to obtain the Context. For details about how to obtain the context, see the usage instructions.
let ctx = Global.abilityContext
let pickerProfile = createPickerProfile(ctx)
getPickerResult(ctx, pickerProfile)
```
