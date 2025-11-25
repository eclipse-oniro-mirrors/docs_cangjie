# Video Playback (Video)

The Video component is used to play video files and control their playback state, commonly employed for short video lists and in-app video pages. It automatically plays when fully displayed, pauses upon user click on the video area, and shows a progress bar that allows seeking to specific positions. For detailed usage, refer to [Video](../reference/arkui-cj/cj-image-video-video.md).

## Creating a Video Component

The Video component is created by calling an interface. For interface invocation methods, see [Creating a Video Component](../reference/arkui-cj/cj-image-video-video.md#creating-the-component).

## Loading Video Resources

The Video component supports loading both local and online videos.

### Loading Local Videos

- Regular Local Videos

To load a local video, first specify the corresponding file in the local rawfile directory as shown below.

![Video](figures/Video.png)

Then reference the video resource using the resource accessor @rawfile().

```cangjie
@Component
class VideoPlayer {
    private var controller: VideoController = VideoController()
    private var previewUris: AppResource = @r(app.media.preview)
    private var innerResource: AppResource = @rawfile("videoTest.mp4")

    func build() {
        Column() {
            Video(src: this.innerResource, previewUri: this.previewUris, controller: this.controller)
        }
    }
}
```

### Loading Sandbox Path Videos

Supports strings with the file:// path prefix for reading resources within the application sandbox path. Ensure the file exists in the sandbox directory and has read permissions.

```cangjie
@Component
class VideoPlayer {
    private var controller: VideoController = VideoController()
    private var videoSrc: String = "file:///data/storage/el2/base/haps/entry/files/show.mp4"

    func build() {
        Column() {
            Video(src: this.videoSrc, controller: this.controller)
        }
    }
}
```

### Loading Online Videos

Loading online videos requires the ohos.permission.INTERNET permission. For permission application methods, refer to [Declaring Permissions](../security/AccessToken/cj-declare-permissions.md). Here, the Video's src attribute is the URL of the online video.

```cangjie
@Component
class VideoPlayer {
    private var controller: VideoController = VideoController()
    private var previewUris: AppResource = @r(app.media.preview)
    private var videoSrc: String = "https://www.example.com/example.mp4" // Replace with actual video URL when used

    func build() {
        Column() {
            Video(src: this.videoSrc, previewUri: this.previewUris, controller: this.controller)
        }
    }
}
```

## Adding Attributes

Video component [attributes](../reference/arkui-cj/cj-image-video-video.md#component-attributes) primarily configure playback behavior, such as muting, displaying control bars, etc.

```cangjie
@Component
class VideoPlayer {
    private var controller: VideoController = VideoController()

    func build() {
        Column() {
            Video(controller: this.controller)
                .muted(false) // Set whether to mute
                .controls(false) // Set whether to show default controls
                .autoPlay(false) // Set whether to autoplay
                .loop(false) // Set whether to loop
                .objectFit(ImageFit.Contain) // Set video scaling mode
        }
    }
}
```

## Event Invocation

Video component callback events include playback start, pause/end, playback failure, playback stop, video preparation, and progress bar operations. It also supports general events like clicks and touches. For details, see [Event Description](../reference/arkui-cj/cj-image-video-video.md#component-events).

```cangjie
@Component
class VideoPlayer {
    private var controller: VideoController = VideoController()
    private var previewUris: AppResource = @r(app.media.preview)
    private var innerResource: AppResource = @rawfile("videoTest.mp4")

    func build() {
        Column() {
            Video(src: this.innerResource, previewUri: this.previewUris, controller: this.controller)
                .onUpdate({ value => // Update event callback
                    Hilog.info(0, "cangjie", "video update.")
                })
                .onPrepared({ value => // Preparation event callback
                    Hilog.info(0, "cangjie", "video prepared.")
                })
                .onError({ => // Error event callback
                    Hilog.info(0, "cangjie", "video error.")
                })
        }
    }
}
```

## Using Video Controllers

Video controllers primarily manage video states, including play, pause, stop, and seeking. For details, see [VideoController Usage](../reference/arkui-cj/cj-image-video-video.md#class-videocontroller).

- Default Controller

  The default controller supports basic functions: play, pause, seeking, and fullscreen display.

    <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry

  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*
  import ohos.resource.*

  @Entry
  @Component
  class EntryView {
      @State var videoSrc: AppResource = @r(app.media.startIcon) // Requires valid video source
      @State var previewUri: AppResource = @r(app.media.startIcon)
      @State var curRate: PlaybackSpeed = PlaybackSpeed.SpeedForward100X

      func build() {
          Row() {
              Column() {
                  Video(src: this.videoSrc, previewUri: this.previewUri, currentProgressRate: this.curRate)
              }
              .width(100.percent)
          }
          .height(100.percent)
      }
  }
  ```

- Custom Controller

  For custom controllers, first disable the default controls, then use components like [button](./cj-common-components-button.md) and [slider](../reference/arkui-cj/cj-button-picker-slider.md) for customized control and display, suitable for highly customized scenarios.

    <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry

  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*
  import ohos.resource.*

  @Entry
  @Component
  class EntryView {
      @State var videoSrc: AppResource = @r(app.media.startIcon) // Requires valid video source
      @State var previewUri: AppResource = @r(app.media.startIcon)
      @State var curRate: PlaybackSpeed = PlaybackSpeed.SpeedForward100X
      @State var isAutoPlay: Bool = false
      @State var showControls: Bool = true
      @State var sliderStartTime: String = ""
      @State var currentTime: Int32 = 0
      @State var durationTime: Int32 = 0
      var controller: VideoController = VideoController()
      func build() {
          Row() {
              Column() {
                  Video(src: this.videoSrc, previewUri: this.previewUri, currentProgressRate: this.curRate,
                      controller: this.controller)
                      .controls(false)
                      .autoPlay(true)
                      .onPrepared({
                              value => this.durationTime = value.duration
                          })
                      .onUpdate({
                              value => this.currentTime = value.time
                          })
                  Row() {
                      Text("${this.currentTime}s")
                      Slider(value: Float64(this.currentTime),  min: 0.0, max: Float64(this.durationTime))
                          .onChange({ value: Float64, mode: SliderChangeMode =>
                                  this.controller.setCurrentTime(Int32(value), SeekMode.Accurate)
                              })
                          .width(85.percent)
                      Text("${this.durationTime}s")
                  }
                  .opacity(0.8)
                  .width(100.percent)
              }.width(100.percent)
          }.height(100.percent)
      }
  }
  ```

## Additional Notes

The Video component encapsulates basic video playback capabilities. Developers don't need to create video instances or handle video information settings—simply configure the data source and basic information to play videos, though this limits extensibility.