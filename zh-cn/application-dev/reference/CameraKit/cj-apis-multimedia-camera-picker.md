# ohos.multimedia.camera_picker（相机选择器）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

camera_picker模块提供拉起系统相机选择照片或视频的能力，应用调用该模块的接口后，系统将拉起相机交互界面，用户完成拍摄和确认后，应用获取对应的照片或视频。

由于照片的拍摄和确认都是由用户进行主动确认，因此应用调用相机选择器时无需申请相机权限。

本模块错误码及相机通用错误码的详细介绍请参见[Camera错误码](./cj-errorcode-multimedia-camera.md)。

## 导入模块

```cangjie
import kit.CameraKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func pick(UIAbilityContext, Array\<PickerMediaType>, PickerProfile, AsyncCallback\<PickerResult>)

```cangjie
public func pick(context: UIAbilityContext, mediaTypes: Array<PickerMediaType>, pickerProfile: PickerProfile,
    callback: AsyncCallback<PickerResult>): Unit
```

**功能：** 拉起相机选择器，并根据媒体类型进入对应模式。该接口使用异步回调返回处理结果。

> **说明：**
>
> 当应用运行在宽屏折叠设备上，且在设备展开时拉起相机选择器，设备由展开态切换到折叠态时，相机选择器会自动移到后台。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|应用上下文。|
|mediaTypes|Array\<[PickerMediaType](#enum-pickermediatype)>|是|-|媒体类型。|
|pickerProfile|[PickerProfile](#class-pickerprofile)|是|-|相机选择器配置。|
|callback|AsyncCallback\<[PickerResult](#class-pickerresult)>|是|-|用于返回相机选择器处理结果的回调。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

let ctx = Global.abilityContext // 此处需手动配置模板，获取Context上下文。上下文获取方式请参见使用说明。
let profile = PickerProfile(CameraPosition.CameraPositionBack)
let callback: AsyncCallback<PickerResult> = {
    err: Option<BusinessException>, data: Option<PickerResult> =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "pick error: code=${e.code}, message=${e.message}")
    } else if (let Some(result) <- data) {
        Hilog.info(0, "test", "resultCode=${result.resultCode}, resultUri=${result.resultUri}")
    }
}
pick(ctx, [PickerMediaType.Photo], profile, callback)
```

## class PickerProfile

```cangjie
public class PickerProfile {
    public mut prop cameraPosition: camera.CameraPosition
    public mut prop saveUri: ?String
    public mut prop videoDuration: ?Int32
    public init(cameraPosition: camera.CameraPosition, saveUri!: ?String = None, videoDuration!: ?Int32 = None)
}
```

**功能：** 相机选择器配置信息。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

### prop cameraPosition

```cangjie
public mut prop cameraPosition: camera.CameraPosition
```

**功能：** 相机位置。

**类型：** [camera.CameraPosition](./cj-apis-multimedia-camera.md#enum-cameraposition)

**读写能力：** 可读写

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

### prop saveUri

```cangjie
public mut prop saveUri: ?String
```

**功能：** 保存配置信息的URI。未指定时，照片和视频自动保存到媒体库；指定时，应使用应用沙箱内可写文件的路径。使用自定义资源路径时，需确保文件存在且可写，否则保存失败。

**类型：** ?String

**读写能力：** 可读写

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

### prop videoDuration

```cangjie
public mut prop videoDuration: ?Int32
```

**功能：** 最大视频时长，单位为秒。未设置或值为0时，表示不限制最大视频时长。

**类型：** ?Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

### init(camera.CameraPosition, ?String, ?Int32)

```cangjie
public init(cameraPosition: camera.CameraPosition, saveUri!: ?String = None, videoDuration!: ?Int32 = None)
```

**功能：** 创建相机选择器配置对象。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|cameraPosition|camera.[CameraPosition](./cj-apis-multimedia-camera.md#enum-cameraposition)|是|-|相机位置。|
|saveUri|?String|否|None|**命名参数。** 保存配置信息的URI。|
|videoDuration|?Int32|否|None|**命名参数。** 最大视频时长，单位为秒。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.PerformanceAnalysisKit.Hilog

let profile = PickerProfile(CameraPosition.CameraPositionBack, videoDuration: Some(10))
Hilog.info(0, "test", "PickerProfile created: ${profile.cameraPosition}")
```

## class PickerResult

```cangjie
public class PickerResult {
    public mut prop resultCode: Int32
    public mut prop resultUri: String
    public mut prop mediaType: PickerMediaType
}
```

**功能：** 相机选择器处理结果。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

### prop mediaType

```cangjie
public mut prop mediaType: PickerMediaType
```

**功能：** 媒体类型。

**类型：** [PickerMediaType](#enum-pickermediatype)

**读写能力：** 可读写

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

### prop resultCode

```cangjie
public mut prop resultCode: Int32
```

**功能：** 结果码。0表示处理成功，-1表示处理失败。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

### prop resultUri

```cangjie
public mut prop resultUri: String
```

**功能：** 结果URI。`saveUri`为空时，`resultUri`为公共媒体路径；`saveUri`不为空且应用具有该URI的写权限时，`resultUri`与`saveUri`相同；`saveUri`不为空但应用不具有写权限时，无法获取`resultUri`。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

## enum PickerMediaType

```cangjie
public enum PickerMediaType {
    | Photo
    | Video
    | ...
}
```

**功能：** 相机选择器支持的媒体类型。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

**父类型：**

- Equatable\<[PickerMediaType](#enum-pickermediatype)>
- ToString

### Photo

```cangjie
Photo
```

**功能：** 照片模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

### Video

```cangjie
Video
```

**功能：** 视频模式。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将媒体类型转换为字符串表示。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|媒体类型的字符串表示。|

### func ==(PickerMediaType)

```cangjie
public operator func ==(other: PickerMediaType): Bool
```

**功能：** 判断两个媒体类型是否相等。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PickerMediaType](#enum-pickermediatype)|是|-|待比较的媒体类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func !=(PickerMediaType)

```cangjie
public operator func !=(other: PickerMediaType): Bool
```

**功能：** 判断两个媒体类型是否不相等。

**系统能力：** SystemCapability.Multimedia.Camera.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PickerMediaType](#enum-pickermediatype)|是|-|待比较的媒体类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|
