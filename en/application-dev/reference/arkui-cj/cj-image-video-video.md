# Video

A component for playing video files and controlling their playback state.

> **Note:**
>
> The Video component only provides basic video playback functionality and cannot support complex video playback control scenarios.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Permission List

When using network videos, the ohos.permission.INTERNET permission must be requested.

## Child Components

Does not support child components.

## Creating the Component

### init(?ResourceStr, ?PlaybackSpeed, ?ResourceStr, ?VideoController)

```cangjie
public init(
    src!: ?ResourceStr = None,
    currentProgressRate!: ?PlaybackSpeed = Option.None,
    previewUri!: ?ResourceStr = None,
    controller!: ?VideoController = None
)
```

**Function:** Creates a video component based on the video data source, playback speed, preview image, and video controller.

**Required Permission:** ohos.permission.INTERNET when using network videos.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| src | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** The data source of the video, supporting local and network videos. |
| currentProgressRate | ?[PlaybackSpeed](./cj-common-types.md#enum-playbackspeed) | No | Option.None | **Named parameter.** The playback speed of the video.<br>Initial value: SpeedForward100X. |
| previewUri | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** The path of the preview image displayed when the video is not playing. |
| controller | ?[VideoController](#class-videocontroller) | No | None | **Named parameter.** Sets the video controller to manage the playback state.<br>Initial value: VideoController() |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func autoPlay(?Bool)

```cangjie
public func autoPlay(value: ?Bool): This
```

**Function:** Sets whether the video plays automatically.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Bool | Yes | - | Whether the video plays automatically.<br>Initial value: false. |

### func controls(?Bool)

```cangjie
public func controls(value: ?Bool): This
```

**Function:** Sets whether the control bar for video playback is displayed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Bool | Yes | - | Whether the control bar is displayed.<br>Initial value: true. |

### func loop(?Bool)

```cangjie
public func loop(value: ?Bool): This
```

**Function:** Sets whether a single video loops.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Bool | Yes | - | Whether the video loops.<br>Initial value: false. |

### func muted(?Bool)

```cangjie
public func muted(value: ?Bool): This
```

**Function:** Sets whether the video is muted.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Bool | Yes | - | Whether the video is muted.<br>Initial value: false. |

### func objectFit(?ImageFit)

```cangjie
public func objectFit(value: ?ImageFit): This
```

**Function:** Sets the video fill mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ImageFit](./cj-common-types.md#enum-imagefit) | Yes | - | The video fill mode.<br>Initial value: ImageFit.Cover. |

## Component Events

### func onError(?VoidCallback)

```cangjie
public func onError(event: ?VoidCallback): This
```

**Function:** Triggered when playback fails.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | Yes | - | Callback function triggered when playback fails.<br>Initial value: { => } |

### func onFinish(?VoidCallback)

```cangjie
public func onFinish(event: ?VoidCallback): This
```

**Function:** Triggered when playback ends.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | Yes | - | Callback function triggered when playback ends.<br>Initial value: { => } |

### func onPause(?VoidCallback)

```cangjie
public func onPause(event: ?VoidCallback): This
```

**Function:** Triggered when playback is paused.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | Yes | - | Callback function triggered when playback is paused.<br>Initial value: { => } |

### func onPrepared(?Callback\<PreparedInfo, Unit>)

```cangjie
public func onPrepared(callback: ?Callback<PreparedInfo, Unit>): This
```

**Function:** Triggered when video preparation is complete.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback](./cj-common-types.md#type-callbackt-v)\<[PreparedInfo](#class-preparedinfo), Unit> | Yes | - | Callback function triggered when video preparation is complete.<br>Initial value: { _ => } |

### func onSeeked(?Callback\<PlaybackInfo, Unit>)

```cangjie
public func onSeeked(callback: ?Callback<PlaybackInfo, Unit>): This
```

**Function:** Triggered after seeking is completed, reporting playback time information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback](./cj-common-types.md#type-callbackt-v)\<[PlaybackInfo](#class-playbackinfo), Unit> | Yes | - | Callback function triggered after seeking is completed.<br>Initial value: { _ => } |

### func onSeeking(?Callback\<PlaybackInfo, Unit>)

```cangjie
public func onSeeking(callback: ?Callback<PlaybackInfo, Unit>): This
```

**Function:** Triggered during seeking, reporting time information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback](./cj-common-types.md#type-callbackt-v)\<[PlaybackInfo](#class-playbackinfo), Unit> | Yes | - | Callback function triggered during seeking.<br>Initial value: { _ => } |

### func onStart(?VoidCallback)

```cangjie
public func onStart(event: ?VoidCallback): This
```

**Function:** Triggered when playback starts.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | Yes | - | Callback function triggered when playback starts.<br>Initial value: { => } |

### func onUpdate(?Callback\<PlaybackInfo, Unit>)

```cangjie
public func onUpdate(callback: ?Callback<PlaybackInfo, Unit>): This
```

**Function:** Triggered when playback progress changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback](./cj-common-types.md#type-callbackt-v)\<[PlaybackInfo](#class-playbackinfo), Unit> | Yes | - | Callback function triggered when playback progress changes.<br>Initial value: { _ => } |

### func onFullscreenChange(?Callback\<FullscreenInfo, Unit>)

```cangjie
public func onFullscreenChange(callback: ?Callback<FullscreenInfo, Unit>): This
```

**Function:** Triggered when the video enters or exits fullscreen mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback](./cj-common-types.md#type-callbackt-v)\<[FullscreenInfo](#class-fullscreeninfo), Unit> | Yes | - | Callback function triggered when the video enters or exits fullscreen mode.<br>Initial value: { _ => } |

## Basic Type Definitions

### class FullscreenInfo

```cangjie
public class FullscreenInfo {
    public var fullscreen: ?Bool
}
```

**Function:** Describes whether the video is in fullscreen playback mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

#### var fullscreen: ?Bool

**Function:** Indicates whether the video is in fullscreen playback mode.

**Initial Version:** 22

### class PlaybackInfo

```cangjie
public class PlaybackInfo {
    public var time: ?Int32
}
```

**Function:** Describes the current playback progress of the video.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

#### var time: ?Int32

**Function:** The current playback progress of the video. Unit: seconds.

**Initial Version:** 22

### class PreparedInfo

```cangjie
public class PreparedInfo {
    public var duration: ?Int32
}
```

**Function:** Describes the duration of the current video.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

#### var duration: ?Int32

**Function:** The duration of the current video. Unit: seconds.

**Initial Version:** 22

### class VideoController

```cangjie
public class VideoController {
    public init()
    public func start(): Unit
    public func pause(): Unit
    public func stop(): Unit
    public func setCurrentTime(value: Int32, seekMode: ?SeekMode): Unit
    public func requestFullscreen(value: ?Bool): Unit
    public func exitFullscreen(): Unit
}
```

**Function:** Video controller.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

#### init()

```cangjie
public init()
```

**Function:** Constructor for VideoController.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

#### func exitFullscreen()

```cangjie
public func exitFullscreen(): Unit
```

**Function:** Exits fullscreen playback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

#### func pause()

```cangjie
public func pause(): Unit
```

**Function:** Pauses playback, displaying the current frame. Playback resumes from the current position when restarted.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

#### func requestFullscreen(?Bool)

```cangjie
public func requestFullscreen(value: ?Bool): Unit
```

**Function:** Requests fullscreen playback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Bool | Yes | - | Whether to play in fullscreen mode.<br>Initial value: false. |

#### func setCurrentTime(Int32, ?SeekMode)

```cangjie
public func setCurrentTime(value: Int32, seekMode: ?SeekMode): Unit
```

**Function:** Sets the playback position of the video.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | Playback time. |
| seekMode | ?[SeekMode](./cj-common-types.md#enum-seekmode) | Yes | - | Seek mode. |

#### func start()

```cangjie
public func start(): Unit
```

**Function:** Starts playback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

#### func stop()

```cangjie
public func stop(): Unit
```

**Function:** Stops playback, displaying the current frame. Playback starts from the beginning when restarted.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22## Example Code

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.i18n.*
import ohos.resource.*
import ohos.arkui.state_macro_manage.*

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

![video](figures/imageVideo.gif)