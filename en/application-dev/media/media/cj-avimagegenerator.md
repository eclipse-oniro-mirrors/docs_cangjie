# Extracting Video Frames at Specified Timestamps Using AVImageGenerator (Cangjie)

The AVImageGenerator can be used to obtain thumbnails from original media assets at specified video timestamps. This development guide demonstrates AVImageGenerator's functionality through an example of extracting thumbnails from a video asset.

The complete workflow for obtaining video thumbnails includes: creating an AVImageGenerator object, setting up the resource, fetching thumbnails, and releasing resources.

## Development Steps and Precautions

For detailed API documentation, refer to [AVImageGenerator API Reference](../../reference/MediaKit/cj-apis-multimedia_media.md#class-avimagegenerator).

1. Create an instance using createAVImageGenerator().

2. Set up the resource: The fdSrc property (representing file descriptor) must be configured.

   > **Note:**
   >
   > Developers should verify resource validity and set fdSrc according to actual scenarios:
   >
   > - Use ResourceManager.getRawFd to open HAP resource file descriptors. For usage, see [ResourceManager API Reference](../../reference/LocalizationKit/cj-apis-resource_manager.md#func-getrawfdstring).
   >
   > - Alternatively, access resources through application sandbox paths (must ensure resource files are available). See [Obtaining Application File Paths](../../file-management/cj-app-sandbox-directory.md#应用文件目录与应用文件路径). For sandbox introduction and file pushing methods, refer to [File Management](../../file-management/cj-app-sandbox-directory.md).
   >
   > - When different AVImageGenerator or [AVMetadataExtractor](../../reference/MediaKit/cj-apis-multimedia_media.md#class-avmetadataextractor) instances need to operate on the same resource, open file descriptors multiple times—do not share the same file descriptor.

3. Retrieve frame at specified timestamp: Call fetchFrameByTime() to obtain a PixelMap object for image display.

4. Release resources: Call release() to destroy the instance and free resources.

## Complete Example

The following example demonstrates setting up a file descriptor and extracting a video thumbnail at a specified timestamp.

<!-- compile -->

```cangjie
// index.cj
import kit.MediaKit.*
import kit.ImageKit.PixelMap
import kit.AbilityKit.*

var ctx = Option<UIAbilityContext>.None

@Entry
@Component
class EntryView {
    @State 
    var message: String = 'Hello World'

    // PixelMap object declaration for image display
    @State 
    var pixelMap: ?PixelMap = Option<PixelMap>.None

    func build() {
        Row() {
            Column() {
                Text(this.message).fontSize(50).fontWeight(FontWeight.Bold)
                Button() {
                    Text('TestButton')
                        .fontSize(30)
                        .fontWeight(FontWeight.Bold)
                }
                .margin(top: 20.px)
                .backgroundColor(0x0D9FFB)
                .width(60.percent)
                .height(5.percent)
                .onClick ({
                    evt =>
                    // Set fdSrc and extract video thumbnail
                    testFetchFrameByTime()
                })
                Image(this.pixelMap).width(300).height(300)
                .margin(top: 20.px)
            }
            .width(100.percent)
            }
            .height(100.percent)
    }

    // Use resource management API to access video files packaged in HAP,
    // configure fdSrc property, extract thumbnails at specified timestamps,
    // and display them via Image component.
    func testFetchFrameByTime() {
        // Create AVImageGenerator object
        let avImageGenerator = createAVImageGenerator()
        // Configure fdSrc
        avImageGenerator.fdSrc = AVFileDescriptor(ctx.getOrThrow().resourceManager.getRawFd('demo.mp4').fd)

        // Initialize parameters
        let timeUs = 0
        let queryOption = AVImageQueryOptions.AV_IMAGE_QUERY_NEXT_SYNC
        let param = PixelMapParams(
            width : 300,
            height : 300
        )

        // Extract thumbnail
        pixelMap = avImageGenerator.fetchFrameByTime(timeUs, queryOption, param)

        // Release resources
        avImageGenerator.release()
        Hilog.info(1, "info", "release success.")
    }
}
```

<!-- compile -->

```cangjie
// main_ability.cj
import ohos.ability.AbilityStage
import ohos.ability.LaunchReason

class MainAbility <: UIAbility {
    public init() {
        super()
        registerSelf()
    }

    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        Hilog.info(1, "info", "MainAbility OnCreated.${want.abilityName}")
        match (launchParam.launchReason) {
            case LaunchReason.START_ABILITY => Hilog.info(1, "info", "START_ABILITY")
            case _ => ()
        }
    }

    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        Hilog.info(1, "info", "MainAbility onWindowStageCreate.")
        windowStage.loadContent("EntryView")
        // declared in index.cj
        ctx = this.context
    }
}
```