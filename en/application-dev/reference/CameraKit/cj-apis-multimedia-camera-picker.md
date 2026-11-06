# ohos.multimedia.camera_picker (Camera Picker)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The camera_picker module provides the capability of launching the system camera to select photos or videos. After the application calls the API of this module, the system displays the camera interaction interface. After the user completes shooting and confirmation, the application obtains the corresponding photo or video.

Since photo shooting and confirmation are both actively performed by the user, the application does not need to apply for the camera permission when calling the camera picker.

For details about the error codes of this module and the common camera error codes, see [Camera Error Codes](./cj-errorcode-multimedia-camera.md).

## Importing the Module

```cangjie
import kit.CameraKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code's first line contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#cangjie-sample-code-notes).

## func pick(UIAbilityContext, Array\<PickerMediaType>, PickerProfile, AsyncCallback\<PickerResult>)

```cangjie
public func pick(context: UIAbilityContext, mediaTypes: Array<PickerMediaType>, pickerProfile: PickerProfile,
    callback: AsyncCallback<PickerResult>): Unit
```

**Description:** Launches the camera picker and enters the corresponding mode based on the media type. This API uses an asynchronous callback to return the result.

> **Note:**
>
> If the application runs on a wide-screen foldable device and the camera picker is launched when the device is unfolded, the camera picker automatically moves to the background when the device is switched from the unfolded state to the folded state.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|Yes|-|Application context.|
|mediaTypes|Array\<[PickerMediaType](#enum-pickermediatype)>|Yes|-|Media type.|
|pickerProfile|[PickerProfile](#class-pickerprofile)|Yes|-|Camera picker configuration.|
|callback|AsyncCallback\<[PickerResult](#class-pickerresult)>|Yes|-|Callback used to return the camera picker result.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CameraKit.*
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

let ctx = Global.abilityContext // The template must be configured manually to obtain the Context. For details about how to obtain the context, see the usage instructions.
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

**Description:** Camera picker configuration information.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

### prop cameraPosition

```cangjie
public mut prop cameraPosition: camera.CameraPosition
```

**Description:** Camera position.

**Type:** [camera.CameraPosition](./cj-apis-multimedia-camera.md#enum-cameraposition)

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

### prop saveUri

```cangjie
public mut prop saveUri: ?String
```

**Description:** URI of the save configuration. If this parameter is not specified, photos and videos are automatically saved to the media library. If it is specified, the path of a writable file in the application sandbox should be used. When a custom resource path is used, ensure that the file exists and is writable. Otherwise, the saving fails.

**Type:** ?String

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

### prop videoDuration

```cangjie
public mut prop videoDuration: ?Int32
```

**Description:** Maximum video duration, in seconds. If this parameter is not set or is set to **0**, the maximum video duration is not limited.

**Type:** ?Int32

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

### init(camera.CameraPosition, ?String, ?Int32)

```cangjie
public init(cameraPosition: camera.CameraPosition, saveUri!: ?String = None, videoDuration!: ?Int32 = None)
```

**Description:** Creates a camera picker configuration object.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|cameraPosition|camera.[CameraPosition](./cj-apis-multimedia-camera.md#enum-cameraposition)|Yes|-|Camera position.|
|saveUri|?String|No|None|**Named parameter.** URI of the save configuration.|
|videoDuration|?Int32|No|None|**Named parameter.** Maximum video duration, in seconds.|

**Example:**

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

**Description:** Camera picker result.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

### prop mediaType

```cangjie
public mut prop mediaType: PickerMediaType
```

**Description:** Media type.

**Type:** [PickerMediaType](#enum-pickermediatype)

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

### prop resultCode

```cangjie
public mut prop resultCode: Int32
```

**Description:** Result code. **0** indicates that the operation is successful, and **-1** indicates that the operation fails.

**Type:** Int32

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

### prop resultUri

```cangjie
public mut prop resultUri: String
```

**Description:** Result URI. If `saveUri` is empty, `resultUri` is a public media path. If `saveUri` is not empty and the application has the write permission on the URI, `resultUri` is the same as `saveUri`. If `saveUri` is not empty but the application does not have the write permission, `resultUri` cannot be obtained.

**Type:** String

**Accessibility:** Read-write

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

## enum PickerMediaType

```cangjie
public enum PickerMediaType {
    | Photo
    | Video
    | ...
}
```

**Description:** Media types supported by the camera picker.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

**Parent Types:**

- Equatable\<[PickerMediaType](#enum-pickermediatype)>
- ToString

### Photo

```cangjie
Photo
```

**Description:** Photo mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

### Video

```cangjie
Video
```

**Description:** Video mode.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Description:** Converts the media type to its string representation.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the media type.|

### func ==(PickerMediaType)

```cangjie
public operator func ==(other: PickerMediaType): Bool
```

**Description:** Checks whether two media types are equal.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[PickerMediaType](#enum-pickermediatype)|Yes|-|Media type to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns **true** if the two enum values are equal; returns **false** otherwise.|

### func !=(PickerMediaType)

```cangjie
public operator func !=(other: PickerMediaType): Bool
```

**Description:** Checks whether two media types are unequal.

**System Capability:** SystemCapability.Multimedia.Camera.Core

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[PickerMediaType](#enum-pickermediatype)|Yes|-|Media type to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns **true** if the two enum values are unequal; returns **false** otherwise.|
