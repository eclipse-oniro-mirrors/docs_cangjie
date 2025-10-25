# Video

A component for playing video files and controlling their playback state.

> **NOTE:**
>
> The Video component only provides basic video playback functionality and cannot support complex video playback control scenarios.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Required Permissions

When using network videos, the ohos.permission.INTERNET permission must be requested.

## Child Components

Does not support child components.

## Creating the Component

### init(ResourceStr, PlaybackSpeed, ResourceStr, VideoController)

```cangjie
public init(
    src!: ResourceStr = "",
    currentProgressRate!: PlaybackSpeed = SpeedForward100X,
    previewUri!: ResourceStr = "",
    controller!: VideoController = VideoController()
)
```

**Function:** Creates a video component based on the video data source, playback speed, preview image, and video controller.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| src | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "" | **Named parameter.** The data source of the video, supporting both local and network videos.<br/>String format can be used to load network and local videos, commonly used for loading network videos.<br/>- Supports network video URLs.<br/>- Supports strings with the file:// path prefix, i.e., application sandbox URI: file://<bundleName>/<sandboxPath>. Used to read resources within the application sandbox path. Ensure the files in the directory path have read permissions.<br/>Supported video formats: mp4, mkv, TS. |
| currentProgressRate | [PlaybackSpeed](#enum-playbackspeed) | No | SpeedForward100X | **Named parameter.** The playback speed of the video.<br/>Supported values: 0.75, 1.0, 1.25, 1.75, 2.0. |
| previewUri | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "" | **Named parameter.** The path of the preview image displayed when the video is not playing. |
| controller | [VideoController](#class-videocontroller) | No | VideoController() | **Named parameter.** Sets the video controller to manage the playback state of the video. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func autoPlay(Bool)

```cangjie
public func autoPlay(value: Bool): This
```

**Function:** Sets whether to auto-play the video.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to auto-play the video.<br>Initial value: false. |

### func controls(Bool)

```cangjie
public func controls(value: Bool): This
```

**Function:** Sets whether to display the video playback control bar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to display the video playback control bar.<br>Initial value: true. |

### func loop(Bool)

```cangjie
public func loop(value: Bool): This
```

**Function:** Sets whether to loop a single video.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to loop a single video.<br>Initial value: false. |

### func muted(Bool)

```cangjie
public func muted(value: Bool): This
```

**Function:** Sets whether to mute the video.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to mute the video.<br>Initial value: false. |

### func objectFit(ImageFit)

```cangjie
public func objectFit(value: ImageFit): This
```

**Function:** Sets the video display mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ImageFit](./cj-common-types.md#enum-imagefit) | Yes | - | The video display mode.<br>Initial value: Cover. |

## Component Events

### func onError(VoidCallback)

```cangjie
public func onError(event: VoidCallback): This
```

**Function:** Triggered when playback fails.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [VoidCallback](../BasicServicesKit/cj-apis-base.md#type-VoidCallback) | Yes | - | Callback function triggered when playback fails. |

### func onFinish(() -> Unit)

```cangjie
public func onFinish(event: () -> Unit): This
```

**Function:** Triggered when playback ends.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ()->Unit | Yes | - | Callback function triggered when playback ends. |

### func onFullscreenChange(Callback\<FullscreenInfo,Unit>)

```cangjie
public func onFullscreenChange(callback: Callback<FullscreenInfo, Unit>): This
```

**Function:** Triggered when switching between full-screen and non-full-screen playback modes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback](../BasicServicesKit/cj-apis-base.md#type-Callback)\<[FullscreenInfo](#class-fullscreeninfo),Unit> | Yes | - | Callback function triggered when switching between full-screen and non-full-screen playback modes. |

### func onPause(VoidCallback)

```cangjie
public func onPause(event: VoidCallback): This
```

**Function:** Triggered when playback is paused.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [VoidCallback](../BasicServicesKit/cj-apis-base.md#type-VoidCallback) | Yes | - | Callback function triggered when playback is paused. |

### func onPrepared(Callback\<PreparedInfo,Unit>)

```cangjie
public func onPrepared(callback: Callback<PreparedInfo, Unit>): This
```

**Function:** Triggered when video preparation is complete.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback](../BasicServicesKit/cj-apis-base.md#type-Callback)\<[PreparedInfo](#class-preparedinfo),Unit> | Yes | - | Callback function triggered when video preparation is complete. |

### func onSeeked(Callback\<PlaybackInfo,Unit>)

```cangjie
public func onSeeked(callback: Callback<PlaybackInfo, Unit>): This
```

**Function:** Triggered after seeking is completed, reporting playback time information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback](../BasicServicesKit/cj-apis-base.md#type-Callback)\<[PlaybackInfo](#class-playbackinfo),Unit> | Yes | - | Callback function triggered after seeking is completed. |

### func onSeeking(Callback\<PlaybackInfo,Unit>)

```cangjie
public func onSeeking(callback: Callback<PlaybackInfo, Unit>): This
```

**Function:** Triggered during seeking, reporting time information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback](../BasicServicesKit/cj-apis-base.md#type-Callback)\<[PlaybackInfo](#class-playbackinfo),Unit> | Yes | - | Callback function triggered during seeking.<br>Parameter value: Current video duration in seconds. |

### func onStart(VoidCallback)

```cangjie
public func onStart(event: VoidCallback): This
```

**Function:** Triggered when playback starts.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [VoidCallback](../BasicServicesKit/cj-apis-base.md#type-VoidCallback) | Yes | - | Callback function triggered when playback starts. |

### func onUpdate(Callback\<PlaybackInfo,Unit>)

```cangjie
public func onUpdate(callback: Callback<PlaybackInfo, Unit>): This
```

**Function:** Triggered when playback progress changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback](../BasicServicesKit/cj-apis-base.md#type-Callback)\<[PlaybackInfo](#class-playbackinfo),Unit> | Yes | - | Callback function triggered when playback progress changes. |

## Basic Type Definitions

### class FullscreenInfo

```cangjie
public class FullscreenInfo {
    public var fullscreen: Bool
}
```

**Function:** Describes whether the video is in full-screen playback mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var fullscreen

```cangjie
public var fullscreen: Bool
```

**Function:** Whether the video is in full-screen playback mode.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

### class PlaybackInfo

```cangjie
public class PlaybackInfo {
    public var time: Int32
}
```

**Function:** Describes the current playback progress of the video.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var time

```cangjie
public var time: Int32
```

**Function:** Current playback progress of the video.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

### class PreparedInfo

```cangjie
public class PreparedInfo {
    public var duration: Int32
}
```

**Function:** Describes the duration of the current video.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var duration

```cangjie
public var duration: Int32
```

**Function:** Duration of the current video.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

### class VideoController

```cangjie
public class VideoController {
    public init()
}
```

**Function:** A VideoController object can control one or more videos.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init()

```cangjie
public init()
```

**Function:** Creates a VideoController object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### func exitFullscreen()

```cangjie
public func exitFullscreen(): Unit
```

**Function:** Exits full-screen playback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### func pause()

```cangjie
public func pause(): Unit
```

**Function:** Pauses playback, displaying the current frame. Playback resumes from the current position when started again.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### func requestFullscreen(Bool)

```cangjie
public func requestFullscreen(value: Bool): Unit
```

**Function:** Requests full-screen playback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to play in full-screen mode (filling the application window). |

#### func setCurrentTime(Int32, SeekMode)

```cangjie
public func setCurrentTime(value: Int32, seekMode: SeekMode): Unit
```

**Function:** Specifies the playback position of the video.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | Playback position of the video.<br/>Unit: s. |
| seekMode | [SeekMode](#enum-seekmode) | Yes | - | Seek mode. |

#### func start()

```cangjie
public func start(): Unit
```

**Function:** Starts playback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### func stop()

```cangjie
public func stop(): Unit
```

**Function:** Stops playback, displaying the current frame. Playback starts from the beginning when started again.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21### enum PlaybackSpeed

```cangjie
public enum PlaybackSpeed <: Equatable<PlaybackSpeed> {
    | SpeedForward075X
    | SpeedForward100X
    | SpeedForward125X
    | SpeedForward175X
    | SpeedForward200X
    | ...
}
```

**Function:** Defines playback speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<PlaybackSpeed>

#### SpeedForward075X

```cangjie
SpeedForward075X
```

**Function:** Plays at 0.75x speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### SpeedForward100X

```cangjie
SpeedForward100X
```

**Function:** Plays at 1x speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### SpeedForward125X

```cangjie
SpeedForward125X
```

**Function:** Plays at 1.25x speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### SpeedForward175X

```cangjie
SpeedForward175X
```

**Function:** Plays at 1.75x speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### SpeedForward200X

```cangjie
SpeedForward200X
```

**Function:** Plays at 2x speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func !=(PlaybackSpeed)

```cangjie
public operator func !=(other: PlaybackSpeed): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PlaybackSpeed](#enum-playbackspeed) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

#### func ==(PlaybackSpeed)

```cangjie
public operator func ==(other: PlaybackSpeed): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PlaybackSpeed](#enum-playbackspeed) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |

### enum SeekMode

```cangjie
public enum SeekMode <: Equatable<SeekMode> {
    | PreviousKeyframe
    | NextKeyframe
    | ClosestKeyframe
    | Accurate
    | ...
}
```

**Function:** Defines seek mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<SeekMode>

#### Accurate

```cangjie
Accurate
```

**Function:** Seeks precisely, regardless of whether it's a keyframe.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### ClosestKeyframe

```cangjie
ClosestKeyframe
```

**Function:** Seeks to the nearest keyframe.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### NextKeyframe

```cangjie
NextKeyframe
```

**Function:** Seeks to the next nearest keyframe.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### PreviousKeyframe

```cangjie
PreviousKeyframe
```

**Function:** Seeks to the previous nearest keyframe.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func !=(SeekMode)

```cangjie
public operator func !=(other: SeekMode): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SeekMode](#enum-seekmode) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

#### func ==(SeekMode)

```cangjie
public operator func ==(other: SeekMode): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SeekMode](#enum-seekmode) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |

## Example Code

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.AppResource

@Entry
@Component
class EntryView {
    var videoSrc: AppResource = @rawfile("video.mp4")
    var previewUri: AppResource = @r(app.media.preview)
    var controller: VideoController = VideoController()
    @State var curRate: PlaybackSpeed = PlaybackSpeed.SpeedForward100X
    @State var isAutoPlay: Bool = false
    @State var showControls: Bool = true

    func build() {
        Column() {
            Video(
                src: this.videoSrc,
                previewUri: this.previewUri,
                currentProgressRate: this.curRate,
                controller: this.controller
            )
                .width(100.percent)
                .height(600)
                .autoPlay(this.isAutoPlay)
                .controls(this.showControls)

            Row() {
                Button("start")
                    .onClick({ evt
                        => this.controller.start() // Start playback
                    })
                    .margin(5)
                    .id("start")
                Button("pause")
                    .onClick({ evt
                        => this.controller.pause() // Pause playback
                    })
                    .margin(5)
                    .id("pause")
                Button("stop")
                    .onClick({ evt
                        => this.controller.stop() // Stop playback
                           this.controller.exitFullscreen()
                        }
                    )
                    .margin(5)
                    .id("stop")
            }
            Row() {
                Button("Fullscreen")
                    .onClick({ evt
                        => this.controller.requestFullscreen(true)
                    })
                    .margin(5)
                    .id("Fullscreen")
                Button("at 10s")
                    .onClick({ evt
                        => this.controller.setCurrentTime(10, SeekMode.ClosestKeyframe)
                    })
                    .margin(5)
                    .id("at 10s")
                Button("exitFull")
                    .onClick({ evt
                        => this.controller.exitFullscreen()
                    })
                    .margin(5)
                    .id("exitFull")
            }
            Row() {
                Button("rate 0.75")
                    .onClick({ evt
                        => this.curRate = PlaybackSpeed.SpeedForward075X
                    })
                    .margin(5)
                    .id("rate 0.75")
                Button("rate 1")
                    .onClick({ evt
                        => this.curRate = PlaybackSpeed.SpeedForward100X
                    })
                    .margin(5)
                    .id("rate 1")
                Button("rate 2")
                    .onClick({ evt
                        => this.curRate = PlaybackSpeed.SpeedForward200X
                    })
                    .margin(5)
                    .id("rate 2")
            }
        }
    }
}
```