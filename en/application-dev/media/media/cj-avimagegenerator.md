# Extracting Video Frames at Specified Times Using AVImageGenerator (Cangjie)

Using [AVImageGenerator](./cj-media-kit-intro.md#avimagegenerator), you can obtain thumbnail images from video media resources at specified timestamps. This development guide demonstrates how to use AVImageGenerator's functionality through an example of extracting a video thumbnail.

The complete process for obtaining video thumbnails includes: creating an AVImageGenerator object, setting the resource, fetching the thumbnail, and releasing resources.

## Development Steps and Precautions

For detailed API documentation, refer to [AVImageGenerator API Reference](../../../../en/application-dev/reference/MediaKit/cj-apis-multimedia_media.md#class-avimagegenerator).

1. Create an instance using createAVImageGenerator().

2. Set the resource: You need to configure the fdSrc property (representing file descriptor).

   > **Note:**
   >
   > Developers should verify resource validity and set fdSrc according to actual scenarios:
   >
   > - You can use ResourceManager.getRawFd to open HAP resource file descriptors. For usage, see [ResourceManager API Reference](../../../../en/application-dev/reference/LocalizationKit/cj-apis-resource_manager.md#func-getrawfdstring).
   >
   > - Alternatively, you can access resources through application sandbox paths (must ensure resource files are available). See [Obtaining Application File Paths](../../file-management/cj-app-sandbox-directory.md#应用文件目录与应用文件路径). For sandbox introduction and file pushing methods, refer to [File Management](../../file-management/cj-app-sandbox-directory.md).
   >
   > - When different AVImageGenerator or [AVMetadataExtractor](../../../../en/application-dev/reference/MediaKit/cj-apis-multimedia_media.md#class-avmetadataextractor) instances need to operate on the same resource, open separate file descriptors rather than sharing one.

3. Retrieve frame at specified time: Call fetchFrameByTime() to obtain a PixelMap object, which can be used for image display.

4. Release resources: Call release() to destroy the instance and free resources.

## Complete Example

The following example demonstrates setting a file descriptor and retrieving a video thumbnail at a specified timestamp.

<!-- compile -->

```cangjie
// index.cj
import kit.MediaKit.*
import kit.ImageKit.*
import kit.AbilityKit.*

var ctx = None<UIAbilityContext>

@Entry
@Component
class EntryView {
    @State message: String = 'Hello World'

    // PixelMap object declaration for image display
    @State pixelMap: ?PixelMap = None

    func build() {
        Row() {
            Column() {
                Text(this.message).fontSize(50).fontWeight(FontWeight.Bold)
                Button() {
                    Text('TestButton')
                        .fontSize(30)
                        .fontWeight(FontWeight.Bold)
                }
                .type(ButtonType.Capsule)
                .margin(top: 20.px)
                .backgroundColor(0x0D9FFB)
                .width(60.percent)
                .height(5.percent)
                .onClick {
                    evt =>
                    // Set fdSrc and retrieve video thumbnail
                    testFetchFrameByTime()
                }
                Image(this.pixelMap).width(300).height(300)
                .margin(top: 20.px)
            }
            .width(100.percent)
            }
            .height(100.percent)
    }

    // Using resource management interface to access video files packaged in HAP,
    // setting fdSrc property to retrieve thumbnails at specified timestamps,
    // and displaying them via Image component.
    func testFetchFrameByTime() {
        // Create AVImageGenerator object
        let avImageGenerator = createAVImageGenerator()
        // Set fdSrc
        avImageGenerator.fdSrc = ctx.getOrThrow().resourceManager.getRawFd('demo.mp4')

        // Initialize parameters
        let timeUs = 0
        let queryOption = AVImageQueryOptions.AV_IMAGE_QUERY_NEXT_SYNC
        let param = PixelMapParams(
            width : 300,
            height : 300
        )

        // Retrieve thumbnail
        pixelMap = avImageGenerator.fetchFrameByTime(timeUs, queryOption, param)

        // Release resources
        avImageGenerator.release()
        AppLog.info("release success.")
    }
}
```

<!-- compile -->

```cangjie
// main_ability.cj
import ohos.base.AppLog
import ohos.ability.AbilityStage
import ohos.ability.LaunchReason

class MainAbility <: UIAbility {
    public init() {
        super()
        registerSelf()
    }

    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        AppLog.info("MainAbility OnCreated.${want.abilityName}")
        match (launchParam.launchReason) {
            case LaunchReason.START_ABILITY => AppLog.info("START_ABILITY")
            case _ => ()
        }
    }

    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        AppLog.info("MainAbility onWindowStageCreate.")
        windowStage.loadContent("EntryView")
        // declared in index.cj
        ctx = this.context
    }
}
```