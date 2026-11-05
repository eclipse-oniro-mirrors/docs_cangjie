# ohos.multimedia.media (Media Services)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The media services module provides developers with a set of simple and easy-to-understand interfaces, enabling convenient access to system media resources.

The media subsystem encompasses audio and video-related media operations, offering the following common functionalities:

- Video thumbnail extraction ([AVImageGenerator](#class-avimagegenerator))

## Importing the Module

```cangjie
import kit.MediaKit.*
```

## Permission List

ohos.permission.MICROPHONE

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration must be done in the "main_ability.cj" file of the Cangjie template project.
- To get the current application sandbox path, use UIAbilityContext.[filesDir](../AbilityKit/cj-apis-app-ability-ui_ability.md#prop-filesdir).

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## func createAVImageGenerator()

```cangjie
public func createAVImageGenerator(): AVImageGenerator
```

**Function:** Creates an AVImageGenerator instance.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| [AVImageGenerator](#class-avimagegenerator) | Video thumbnail extraction class. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Media Error Codes](./cj-errorcode-multimedia-media.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 5400101 | No memory. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaKit.*
import kit.PerformanceAnalysisKit.*
import kit.CangjieKit.BusinessException

try {
    let generator = createAVImageGenerator()
} catch (e: BusinessException) {
    Hilog.error(0, "AppLogCj", e.message)
}
```

## class AVFileDescriptor

```cangjie
public class AVFileDescriptor {
    public var fd: Int32
    public var offset: Int64
    public var length: Int64
    public init(
        fd: Int32,
        offset!: Int64 = 0,
        length!: Int64 = -1
    )
}
```

**Function:** Descriptor for audio/video file resources, a special playback method for specific resources. Usage scenario: When audio resources in an application are stored contiguously in the same file and need to be played based on offset and length.

**System Capability:** SystemCapability.Multimedia.Media.Core

**Since:** 22

### var fd

```cangjie
public var fd: Int32
```

**Function:** Resource handle.

**Type:** Int32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Media.Core

**Since:** 22

### var length

```cangjie
public var length: Int64
```

**Function:** Resource length. Default value is the remaining bytes from the offset in the file. Must be input based on preset resource information. Invalid values will cause audio/video resource parsing errors.

**Type:** Int64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Media.Core

**Since:** 22

### var offset

```cangjie
public var offset: Int64
```

**Function:** Resource offset. Default value is 0. Must be input based on preset resource information. Invalid values will cause audio/video resource parsing errors.

**Type:** Int64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Media.Core

**Since:** 22

### init(Int32, Int64, Int64)

```cangjie
public init(
    fd: Int32,
    offset!: Int64 = 0,
    length!: Int64 = -1
)
```

**Function:** Constructs an audio/video file resource descriptor type.

**System Capability:** SystemCapability.Multimedia.Media.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| fd | Int32 | Yes | - | Resource handle, obtained via [resourceManager.getRawFd](../LocalizationKit/cj-apis-resource_manager.md#func-getrawfdstring). |
| offset | Int64 | No | 0 | **Named parameter.** Resource offset. Must be input based on preset resource information. Invalid values will cause subtitle/audio resource parsing errors. |
| length | Int64 | No | -1 | **Named parameter.** Resource length. Default value is the remaining bytes from the offset in the file. Must be input based on preset resource information. Invalid values will cause subtitle/audio resource parsing errors. |

## class AVImageGenerator

```cangjie
public class AVImageGenerator {}
```

**Function:** Video thumbnail extraction class, used to obtain thumbnails from video resources. Before calling AVImageGenerator methods, an AVImageGenerator instance must first be created via [createAVImageGenerator()](#func-createavimagegenerator).

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

### prop fdSrc

```cangjie
public mut prop fdSrc: AVFileDescriptor
```

**Function:** Media file descriptor. The data source is set via this property.

> **Note:**
>
> After passing the resource handle (fd) to an AVImageGenerator instance, do not perform other read/write operations using this handle, including but not limited to passing the same handle to multiple AVPlayer / AVMetadataExtractor / AVImageGenerator / AVTranscoder instances. Concurrent read/write operations via the same handle may cause race conditions, leading to video thumbnail data extraction failures.

**Type:** [AVFileDescriptor](#class-avfiledescriptor)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

### func fetchFrameByTime(Int64, AVImageQueryOptions, PixelMapParams)

```cangjie
public func fetchFrameByTime(timeUs: Int64, options: AVImageQueryOptions, param: PixelMapParams): PixelMap
```

**Function:** Retrieves a video thumbnail.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| timeUs | Int64 | Yes | - | The timestamp in the video for which to retrieve the thumbnail, in microseconds (μs). |
| options | [AVImageQueryOptions](#enum-avimagequeryoptions) | Yes | - | The relationship between the requested timestamp and the corresponding video frame. |
| param | [PixelMapParams](#class-pixelmapparams) | Yes | - | Format parameters for the requested thumbnail. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap) | Video thumbnail. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Media Error Codes](./cj-errorcode-multimedia-media.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 5400101 | No memory. Create AVImageGenerator failed. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.MediaKit.*
import kit.LocalizationKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let timeUs = 0
    let queryOption = AVImageQueryOptions.AvImageQueryNextSync
    let param = PixelMapParams(width: 300, height: 300)
    let generator = createAVImageGenerator()
    let abilityContext = Global.getAbilityContext() // Application context must be obtained. See usage instructions above.
    let rawFd = Global.getResourceManager().getRawFd("trailer.mp4")    // Replace with your resource path. For file path acquisition, see usage instructions above.
    generator.fdSrc = AVFileDescriptor(rawFd.fd, offset: rawFd.offset, length: rawFd.length)
    let pic = generator.fetchFrameByTime(timeUs, queryOption, param)
    generator.release()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func release()

```cangjie
public func release(): Unit
```

**Function:** Releases resources.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Media Error Codes](./cj-errorcode-multimedia-media.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 5400102 | Operation not allowed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaKit.*
import kit.LocalizationKit.*
import kit.PerformanceAnalysisKit.*
import kit.CangjieKit.BusinessException

try {
    let timeUs = 0
    let queryOption = AVImageQueryOptions.AvImageQueryNextSync
    let param = PixelMapParams(width: 300, height: 300)
    let generator = createAVImageGenerator()
    let abilityContext = Global.getAbilityContext() // Application context must be obtained. See usage instructions above.
    let rawFd = abilityContext.getResourceManager().getRawFd("trailer.mp4")
    generator.fdSrc = AVFileDescriptor(rawFd.fd, offset:rawFd.offset, length:rawFd.length)
    let pic = generator.fetchFrameByTime(timeUs, queryOption, param)
    generator.release()
} catch (e: BusinessException) {
    Hilog.error(0, "AppLogCj", e.message)
}
```

## class PixelMapParams

```cangjie
public class PixelMapParams {
    public var width: Int32
    public var height: Int32
    public init(width!: Int32 = -1, height!: Int32 = -1)
}
```

**Function:** Format parameters for output thumbnails when retrieving video thumbnails.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

### var height

```cangjie
public var height: Int32
```

**Function:** Height of the output thumbnail.

**Type:** Int32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

### var width

```cangjie
public var width: Int32
```

**Function:** Width of the output thumbnail.

**Type:** Int32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

### init(Int32, Int32)

```cangjie
public init(width!: Int32 = -1, height!: Int32 = -1)
```

**Function:** Constructs thumbnail format parameters.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| width | Int32 | No | -1 | **Named parameter.** Width of the output thumbnail. Must be greater than 0 and not exceed the original video width. Otherwise, the returned thumbnail will not be scaled. |
| height | Int32 | No | -1 | **Named parameter.** Height of the output thumbnail. Must be greater than 0 and not exceed the original video height. Otherwise, the returned thumbnail will not be scaled. |

## enum AVImageQueryOptions

```cangjie
public enum AVImageQueryOptions <: Equatable<AVImageQueryOptions> & ToString {
    | AvImageQueryNextSync
    | AvImageQueryPreviousSync
    | AvImageQueryClosestSync
    | AvImageQueryClosest
    | ...
}
```

**Function:** Specifies the relationship between the requested timestamp and the corresponding video frame when retrieving thumbnails.<br/>When obtaining a video thumbnail, the requested timestamp may not exactly match the actual video frame timestamp. This enum defines how the requested timestamp relates to the actual frame timestamp.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

**Parent Types:**

- Equatable\<AVImageQueryOptions>
- ToString

### AvImageQueryClosest

```cangjie
AvImageQueryClosest
```

**Function:** Selects the frame closest to the requested timestamp, which may not necessarily be a keyframe.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22### AvImageQueryClosestSync

```cangjie
AvImageQueryClosestSync
```

**Function:** Selects the keyframe closest to the specified timestamp.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

### AvImageQueryNextSync

```cangjie
AvImageQueryNextSync
```

**Function:** Selects the keyframe at or after the specified timestamp.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

### AvImageQueryPreviousSync

```cangjie
AvImageQueryPreviousSync
```

**Function:** Selects the keyframe at or before the specified timestamp.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

### func !=(AVImageQueryOptions)

```cangjie
public operator func !=(other: AVImageQueryOptions): Bool
```

**Function:** Compares whether two AVImageQueryOptions instances are unequal.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AVImageQueryOptions](#enum-avimagequeryoptions) | Yes | - | Another AVImageQueryOptions instance. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two AVImageQueryOptions are unequal, otherwise returns false. |

### func ==(AVImageQueryOptions)

```cangjie
public operator func ==(other: AVImageQueryOptions): Bool
```

**Function:** Compares whether two AVImageQueryOptions instances are equal.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AVImageQueryOptions](#enum-avimagequeryoptions) | Yes | - | Another AVImageQueryOptions instance. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two AVImageQueryOptions are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of AVImageQueryOptions.

**System Capability:** SystemCapability.Multimedia.Media.AVImageGenerator

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string representation of AVImageQueryOptions. |