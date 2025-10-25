# Image

The Image component is used to display images in applications. It supports image formats including png, jpg, jpeg, bmp, svg, webp, gif, and heif.

> **Notes:**
>
> - When using shortcut keys to copy the Image component, the Image component must be in a [focused state](./cj-universal-attribute-focus.md#func-focusontouchbool). By default, the Image component is not focusable. To enable focus, set the [focusable](cj-apis-window.md#var-focusable) attribute to true, then use the TAB key to shift focus to the component. Set the [focusOnTouch](./cj-universal-attribute-focus.md#func-focusontouchbool) attribute to true to enable focus on click.
> - The supported image formats include SVG sources. For SVG tag documentation, refer to [SVG Tag Description](../ImageKit/cj-apis-image.md#svg标签说明).
> - The playback of animated images depends on the visibility changes of the Image node. By default, animations are not played. When the node becomes visible, the animation starts via a callback, and when the node becomes invisible, the animation stops. The visibility state is determined by the [onVisibleAreaChange](./cj-ui-framework.md#func-onvisibleareachangearrayfloat64-boolfloat64---unit) event. When the visible threshold ratios are greater than 0, the Image is considered visible.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Required Permissions

When using network images, add the internet usage permission `ohos.permission.INTERNET` to the "requestPermissions" section in module.json5.

```json
"requestPermissions": [
    { "name": "ohos.permission.INTERNET"}
]
```

## Child Components

None

## Creating the Component

### init(ResourceStr)

```cangjie
public init(src: ResourceStr)
```

**Function:** Obtains an image from the image data source for subsequent rendering and display.

> **Notes:**
>
> - If the Image component fails to load the image or the image size is 0, the component size automatically becomes 0 and does not follow the parent component's layout constraints.
> - By default, the Image component crops the image from the center. For example, if the component's width and height are set to the same value but the original image's aspect ratio differs, the middle area is cropped.
> - If the Image loads successfully and the component's width and height are not set, its display size adapts to the parent component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| src | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | The data source of the image.<br/>ResourceStr can be used to load network and local images. |

### init(PixelMap)

```cangjie
public init(src: PixelMap)
```

**Function:** Obtains an image from the image data source for subsequent rendering and display.

> **Notes:**
>
> - If the Image component fails to load the image or the image size is 0, the component size automatically becomes 0 and does not follow the parent component's layout constraints.
> - By default, the Image component crops the image from the center. For example, if the component's width and height are set to the same value but the original image's aspect ratio differs, the middle area is cropped.
> - If the Image loads successfully and the component's width and height are not set, its display size adapts to the parent component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| src | [PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap) | Yes | - | The data source of the image.<br/>PixelMap is a pixel map format commonly used in image editing scenarios. |

## Universal Attributes/Events

Universal Attributes: All supported.

> **Notes:**
>
> The Image component does not support setting the universal attribute [foregroundColor](./cj-universal-attribute-foregroundcolor.md#func-foregroundcolorresourcecolor). Instead, use the Image component's [fillColor](#func-fillcolorresourcecolor) attribute to set the fill color.

Universal Events: All supported.

## Component Attributes

### func alt(ResourceStr)

```cangjie
public func alt(src: ResourceStr): This
```

**Function:** Sets the placeholder image displayed during image loading.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| src | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | The placeholder image displayed during loading. Local images (png, jpg, bmp, svg, gif, and heif formats) are not supported; network images are supported. |

### func autoResize(Bool)

```cangjie
public func autoResize(value: Bool): This
```

**Function:** Sets whether to automatically scale the image source during decoding.

> **Notes:**
>
> This operation determines the source size used for drawing based on the display area dimensions, which helps reduce memory usage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to automatically scale the image source during decoding. When set to true, the component determines the source size used for drawing based on the display area dimensions, which helps reduce memory usage. For example, if the original image size is 1920x1080 and the display area size is 200x200, the image will be downsampled to 200x200 during decoding, significantly saving memory.<br/>Default: false. |

### func fillColor(ResourceColor)

```cangjie
public func fillColor(value: ResourceColor): This
```

**Function:** Sets the fill color to replace the SVG image. Only effective for SVG sources.

> **Notes:**
>
> To modify the color of a PNG image, use [colorFilter](#class-colorfilter).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Sets the fill color.<br/>By default, the component is not filled. If an invalid value is passed, the system uses the default theme color: black in light mode and white in dark mode. |

### func fitOriginalSize(Bool)

```cangjie
public func fitOriginalSize(value: Bool): This
```

**Function:** Sets whether the image display size follows the source image size. If the Image component size is not set, its display size follows the source image size.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to follow the source image size.<br/>Default: false. |

### func interpolation(ImageInterpolation)

```cangjie
public func interpolation(value: ImageInterpolation): This
```

**Function:** Sets the interpolation effect for the image.

> **Notes:**
>
> - Reduces aliasing issues when low-resolution images are displayed at larger sizes. Only applies to image upscaling.
> - SVG sources do not support this attribute.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ImageInterpolation](#enum-imageinterpolation) | Yes | - | The interpolation effect for the image.<br/>Default: ImageInterpolation.Low. |

### func matchTextDirection(Bool)

```cangjie
public func matchTextDirection(value: Bool): This
```

**Function:** Sets whether the image follows the system language direction, displaying a mirrored flip effect in RTL language environments.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to follow the system language direction.<br/>Default: false. |

### func objectFit(ImageFit)

```cangjie
public func objectFit(value: ImageFit): This
```

**Function:** Sets the fill effect for the image.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ImageFit](./cj-common-types.md#enum-imagefit) | Yes | - | The fill effect for the image.<br/>Default: ImageFit.Cover. |

### func objectRepeat(ImageRepeat)

```cangjie
public func objectRepeat(value: ImageRepeat): This
```

**Function:** Sets the repeat style for the image.

> **Notes:**
>
> - Repeats from the center outward, truncating if there is insufficient space for another image.
> - SVG sources do not support this attribute.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ImageRepeat](./cj-common-types.md#enum-imagerepeat) | Yes | - | The repeat style for the image.<br/>Default: ImageRepeat.NoRepeat. |

### func renderMode(ImageRenderMode)

```cangjie
public func renderMode(value: ImageRenderMode): This
```

**Function:** Sets the rendering mode for the image.

> **Notes:**
>
> - SVG sources do not support this attribute.
> - When [ColorFilter](#class-colorfilter) is set, this attribute setting does not take effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ImageRenderMode](#enum-imagerendermode) | Yes | - | The rendering mode for the image, either original color or black.<br/>Default: ImageRenderMode.Original. |

### func sourceSize(Length, Length)

```cangjie
public func sourceSize(width: Length, height: Length): This
```

**Function:** Decodes the original image into a PixelMap of the specified size. PixelMap resources do not support this function.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The width of the decoded image.<br>Unit: vp. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The height of the decoded image.<br>Unit: vp. |

### func syncLoad(Bool)

```cangjie
public func syncLoad(value: Bool): This
```

**Function:** Sets whether to load the image synchronously.

> **Notes:**
>
> It is recommended to set `syncLoad` to true when loading small local images, as the operation is quick and can be executed on the main thread.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to load the image synchronously. By default, images are loaded asynchronously. Synchronous loading blocks the UI thread and does not display a placeholder image.<br/>Default: false. |

## Component Events

### func onComplete(ImageCompleteCallback)

```cangjie
public func onComplete(callback: ImageCompleteCallback): This
```

**Function:** Triggered when the image is successfully loaded, returning the dimensions of the successfully loaded image.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | ImageCompleteCallback | Yes | - | The callback function triggered when the image is successfully loaded. |

### func onError(ImageErrorCallback)

```cangjie
public func onError(callback: ImageErrorCallback): This
```

**Function:** Triggered when an error occurs during image loading.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | ImageErrorCallback | Yes | - | The callback function triggered when an error occurs during image loading. |

### func onFinish(() -> Unit)

```cangjie
public func onFinish(event: () -> Unit): This
```

**Function:** When the loaded source file is an animated SVG image, this event is triggered when the SVG animation finishes playing. If the animation is set to loop infinitely, this event will not be triggered.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | () -> Unit | Yes | - | The callback function triggered when the SVG animation finishes playing. |

## Basic Type Definitions

### class ColorFilter

```cangjie
public class ColorFilter {
    public init(array: Array<Float32>)
}
```

**Function:** A color filter matrix.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(Array\<Float32>)

```cangjie
public init(value: Array<Float32>)
```

**Function:** Constructs a color filter matrix.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Array\<Float32> | Yes | - | A 4x5 filter matrix. |### class ImageLoadResult

```cangjie
public class ImageLoadResult {
    public var width: Float64
    public var height: Float64
    public var componentWidth: Float64
    public var componentHeight: Float64
    public var loadingStatus: Int32
    public var contentWidth: Float64
    public var contentHeight: Float64
    public var contentOffsetX: Float64
    public var contentOffsetY: Float64
}
```

**Function:** Image loading success type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var componentHeight

```cangjie
public var componentHeight: Float64
```

**Function:** Height of the component, in px.

**Type:** Float64

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var componentWidth

```cangjie
public var componentWidth: Float64
```

**Function:** Width of the component, in px.

**Type:** Float64

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var contentHeight

```cangjie
public var contentHeight: Float64
```

**Function:** Actual rendered height of the image, in px.

> **Note:**
>
> Only valid when loadingStatus returns 1.

**Type:** Float64

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var contentOffsetX

```cangjie
public var contentOffsetX: Float64
```

**Function:** X-axis offset of the actual rendered content relative to the component itself, in px.

> **Note:**
>
> Only valid when loadingStatus returns 1.

**Type:** Float64

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var contentOffsetY

```cangjie
public var contentOffsetY: Float64
```

**Function:** Y-axis offset of the actual rendered content relative to the component itself, in px.

> **Note:**
>
> Only valid when loadingStatus returns 1.

**Type:** Float64

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var contentWidth

```cangjie
public var contentWidth: Float64
```

**Function:** Actual rendered width of the image, in px.

> **Note:**
>
> Only valid when loadingStatus returns 1.

**Type:** Float64

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var height

```cangjie
public var height: Float64
```

**Function:** Height of the image, in px.

**Type:** Float64

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var loadingStatus

```cangjie
public var loadingStatus: Int32
```

**Function:** Status indicating successful image loading.

**Type:** Int32

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var width

```cangjie
public var width: Float64
```

**Function:** Width of the image, in px.

**Type:** Float64

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### enum ImageInterpolation

```cangjie
public enum ImageInterpolation {
    | None
    | High
    | Medium
    | Low
    | ...
}
```

**Function:** Image interpolation method.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<ImageInterpolation>

#### High

```cangjie
High
```

**Function:** High-quality interpolation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Low

```cangjie
Low
```

**Function:** Low-quality interpolation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Medium

```cangjie
Medium
```

**Function:** Medium-quality interpolation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### None

```cangjie
None
```

**Function:** No interpolation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func !=(ImageInterpolation)

```cangjie
public operator func !=(other: ImageInterpolation): Bool
```

**Function:** Determines whether two enumeration values are not equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ImageInterpolation](#enum-imageinterpolation)|Yes|-|Another enumeration value to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are not equal, otherwise returns false.|

#### func ==(ImageInterpolation)

```cangjie
public operator func ==(other: ImageInterpolation): Bool
```

**Function:** Determines whether two enumeration values are equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ImageInterpolation](#enum-imageinterpolation)|Yes|-|Another enumeration value to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are equal, otherwise returns false.|

### enum ImageRenderMode

```cangjie
public enum ImageRenderMode <: Equatable<ImageRenderMode> {
    | Original
    | Template
    | ...
}
```

**Function:** Image rendering mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<ImageRenderMode>

#### Original

```cangjie
Original
```

**Function:** Renders the image as-is, including colors.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Template

```cangjie
Template
```

**Function:** Renders the image as a template, ignoring color information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func !=(ImageRenderMode)

```cangjie
public operator func !=(other: ImageRenderMode): Bool
```

**Function:** Determines whether two enumeration values are not equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ImageRenderMode](#enum-imagerendermode)|Yes|-|Another enumeration value to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are not equal, otherwise returns false.|

#### func ==(ImageRenderMode)

```cangjie
public operator func ==(other: ImageRenderMode): Bool
```

**Function:** Determines whether two enumeration values are equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ImageRenderMode](#enum-imagerendermode)|Yes|-|Another enumeration value to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are equal, otherwise returns false.|

## type ImageCompleteCallback

```cangjie
public type ImageCompleteCallback =(ImageLoadResult) -> Unit
```

**Function:** Callback function type for image loading completion.

## type ImageErrorCallback

```cangjie
public type ImageErrorCallback =(ImageError) -> Unit
```

**Function:** Callback function type for image loading errors.

## Example Code

### Example 1 (Loading Basic Image Types)

Loading basic image types such as png, gif, svg, and jpg.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.AppResource

@Entry
@Component
class EntryView {
    func build() {
        Flex(direction: FlexDirection.Column, alignItems: ItemAlign.Start) {
                Row() {
                    // Load png format image
                    Image(@r(app.media.startIcon))
                    .width(110)
                    .height(110)
                    .margin(15)
                    .overlay(value: "png", align: Alignment.Bottom, offset: OverlayOffset(x: 0.0, y: 20.0))
                    // Load gif format image
                    Image(@r(app.media.list))
                    .width(110).height(110).margin(15)
                    .overlay(value: "gif", align: Alignment.Bottom, offset: OverlayOffset(x: 0.0, y: 20.0))
                }
                Row() {
                    // Load svg format image
                    Image(@r(app.media.svg))
                    .width(110)
                    .height(110)
                    .margin(15)
                    .overlay(value: "svg", align: Alignment.Bottom, offset: OverlayOffset(x: 0.0, y: 20.0))
                    // Load jpg format image
                    Image(@r(app.media.startIcon_jpg))
                    .width(110)
                    .height(110)
                    .margin(15)
                    .overlay(value: "jpg", align: Alignment.Bottom, offset: OverlayOffset(x: 0.0, y: 20.0))
                }
            }
            .height(320)
            .width(360)
            .padding(right: 10, top: 10)
    }
}
```

![image1](figures/image1.gif)### Example 2 (Adding Events to Images)

Adding onClick and onFinish events to images.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.AppResource

@Entry
@Component
class EntryView {
    let imageOne: AppResource= @r(app.media.startIcon)
    let imageTwo = @r(app.media.background)
    let imageThree = @r(app.media.svg_move)
    @State var src: AppResource = this.imageOne
    @State var src2: AppResource = this.imageThree

    func build() {
        Column(){
            // Add click event to image, load specific image after click
            Image(this.src)
            .width(100)
            .height(100)
            .onClick{
                    evt =>
                    this.src =this.imageTwo
            }
            // When loading SVG format images
            Image(this.src2)
            .width(100)
            .height(100)
            .onFinish{
                    // Load another image after SVG animation completes
                    =>
                    this.src2 =this.imageOne
            }
        }
    }
}
```

![image2](figures/image2.gif)

### Example 3 (Setting Image Fill Effects)

This example demonstrates setting fill effects for images using objectFit.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.AppResource

@Entry
@Component
class EntryView {
    func build() {
        Flex(direction: FlexDirection.Column, alignItems: ItemAlign.Start) {
            Row() {
                // Load PNG format image
                Image(@r(app.media.view))
                .width(110)
                .height(110)
                .margin(15)
                .overlay(value: "Contain", align: Alignment.Bottom, offset: OverlayOffset(x: 0.0, y: 20.0))
                .border(width: 2, color: 0xFEC0CD)
                .objectFit(ImageFit.Contain)
                // Load GIF format image
                Image(@r(app.media.view))
                .width(110)
                .height(110)
                .margin(15)
                .overlay(value: "Cover", align: Alignment.Bottom, offset: OverlayOffset(x: 0.0, y: 20.0))
                .border(width: 2, color: 0xFEC0CD)
                .objectFit(ImageFit.Cover)
            }
            Row() {
                // Load SVG format image
                Image(@r(app.media.view))
                .width(110)
                .height(110)
                .margin(15)
                .overlay(value: "Fill", align: Alignment.Bottom, offset: OverlayOffset(x: 0.0, y: 20.0))
                .border(width: 2, color: 0xFEC0CD)
                .objectFit(ImageFit.Fill)
                // Load JPG format image
                Image(@r(app.media.startIcon))
                .width(110)
                .height(110)
                .margin(15)
                .overlay(value: "ScaleDown", align: Alignment.Bottom, offset: OverlayOffset(x: 0.0, y: 20.0))
                .border(width: 2, color: 0xFEC0CD)
                .objectFit(ImageFit.ScaleDown)
            }
            Row() {
                // Load PNG format image
                Image(@r(app.media.view))
                .width(110)
                .height(110)
                .margin(15)
                .overlay(value: "Auto", align: Alignment.Bottom, offset: OverlayOffset(x: 0.0, y: 20.0))
                .border(width: 2, color: 0xFEC0CD)
                .objectFit(ImageFit.Auto)
                // Load GIF format image
                Image(@r(app.media.view))
                .width(110)
                .height(110)
                .margin(15)
                .overlay(value: "None", align: Alignment.Bottom, offset: OverlayOffset(x: 0.0, y: 20.0))
                .border(width: 2, color: 0xFEC0CD)
                .objectFit(ImageFit.None)
            }
        }
        .height(480)
        .width(360)
        .padding(right: 10, top: 10)
    }
}
```

![image4](figures/image10.jpg)

### Example 4 (Switching Between Different Image Types)

This example demonstrates displaying effects when using PNG and SVG formats as data sources.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.AppResource

@Entry
@Component
class EntryView {
    let imageOne: AppResource= @r(app.media.startIcon)
    let imageTwo = @r(app.media.svg_move)
    @State var imageSrcIndex : Int64 = 0
    @State var imageSrcList : Array<AppResource> = [this.imageOne,this.imageTwo]

    func build() {
        Column(){
            Image(this.imageSrcList[this.imageSrcIndex])
                .width(100)
                .height(100)
            Button("Click to switch Image src")
                .padding(20)
                .onClick{
                    evt =>
                    this.imageSrcIndex = (this.imageSrcIndex + 1) % 2
            }
        }
    }
}
```

![image5](figures/image5.gif)

### Example 5 (Setting Image Decoding Size via sourceSize)

This example demonstrates customizing image decoding size using the [sourceSize](#func-sourcesizelength-length) interface.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.AppResource
import ohos.arkui.component.ImageFit

@Entry
@Component
class EntryView {
    @State var borderRadiusValue : Int64 = 10

    func build() {
        Column(){
            Image(@r(app.media.image))
                .sourceSize(500,500)
                .width(300)
                .height(300)
            Image(@r(app.media.image))
                .sourceSize(10,10)
                .width(300)
                .height(300)
                .borderWidth(1)
        }
        .height(100.percent)
        .width(100.percent)
    }
}
```

![image6](figures/image6_api.png)

### Example 6 (Setting Image Rendering Mode via renderMode)

This example demonstrates setting image rendering mode to grayscale using the [renderMode](#func-rendermodeimagerendermode) interface.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.AppResource
import ohos.arkui.component.ImageFit

@Entry
@Component
class EntryView {
    @State var borderRadiusValue : Int64 = 10

    func build() {
        Column(){
            Image(@r(app.media.image))
                .renderMode(ImageRenderMode.Template)
                .width(300)
                .height(300)
        }
        .height(100.percent)
        .width(100.percent)
    }
}
```

![image7](figures/image7_api.png)

### Example 7 (Setting Image Repeat Style via objectRepeat)

This example demonstrates repeating image drawing on the vertical axis using the [objectRepeat](#func-objectrepeatimagerepeat) interface.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.AppResource
import ohos.arkui.component.ImageFit

@Entry
@Component
class EntryView {
    @State var borderRadiusValue : Int64 = 10
    func build() {
        Column(){
            Image(@r(app.media.image))
                .objectRepeat(ImageRepeat.Y)
                .width(120)
                .height(300)
                .objectFit(ImageFit.Contain)
                .borderWidth(1)
        }
        .height(100.percent)
        .width(100.percent)
    }
}
```

![image8](figures/image8.png)

### Example 8 (Setting Fill Color for SVG Images)

This example demonstrates repeating image drawing on the vertical axis using the [fillColor](#func-fillcolorresourcecolor) interface.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.AppResource

@Entry
@Component
class EntryView {
    @State var borderRadiusValue : Int64 = 10
    func build() {
        Column(){
            Text("Without fillColor")
            Image(@r(app.media.svg))
                .width(100)
                .height(100)
                .objectFit(ImageFit.Contain)
                .borderWidth(1)
            Text("fillColor set to Color.Gray")
            Image(@r(app.media.svg))
                .width(100)
                .height(100)
                .objectFit(ImageFit.Contain)
                .borderWidth(1)
                .fillColor(Color.Gray)
            Text("fillColor set to Color.Blue")
            Image(@r(app.media.svg))
                .width(100)
                .height(100)
                .objectFit(ImageFit.Contain)
                .borderWidth(1)
                .fillColor(Color.Blue)
            Text("fillColor set to Color.Red")
            Image(@r(app.media.svg))
                .width(100)
                .height(100)
                .objectFit(ImageFit.Contain)
                .borderWidth(1)
                .fillColor(Color.Red)
        }
        .height(100.percent)
        .width(100.percent)
    }
}
```

![image9](figures/image9.png)