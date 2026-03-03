# ohos.multimedia.image (Image Processing)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module provides image processing capabilities, including creating PixelMap through properties, reading image pixel data, and extracting image data within specified regions.

## Importing the Module

```cangjie
import kit.ImageKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code begins with a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration must be done in the "main_ability.cj" file of the Cangjie template project.
- When running sample code, first construct the correct image source through [createImageSource](#func-createimagesourcestring-sourceoptions), which supports building image sources from raw arrays, URIs, file descriptors, etc.

For details about the sample project and configuration template, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## func createImagePacker()

```cangjie
public func createImagePacker(): ImagePacker
```

**Description:** Creates an ImagePacker instance.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
|[ImagePacker](#class-imagepacker)|Returns an ImagePacker instance.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let imagePacker : ImagePacker = createImagePacker()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createImageReceiver(Size, ImageFormat, Int32)

```cangjie
public func createImageReceiver(size: Size, format: ImageFormat, capacity: Int32): ImageReceiver
```

**Description:** Creates an ImageReceiver instance with specified width, height, image format, and capacity.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|size|[Size](#class-size)|Yes|-|Default size of the image.|
|format|[ImageFormat](#enum-imageformat)|Yes|-|Image format, using constants from [ImageFormat](#enum-imageformat) (currently only ImageFormat:JPEG is supported).|
|capacity|Int32|Yes|-|Maximum number of images that can be accessed simultaneously.|

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageReceiver](#class-imagereceiver)|Returns an ImageReceiver instance if the operation succeeds.|

**Exceptions:**

- BusinessException: Error codes as shown below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980104 | Failed to initialize the internal object. |
  | 62980115 | Parameter error. Possible causes: 1. Mandatory parameters are unspecified; 2. Incorrect parameter types. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let size = Size(8, 8192)
    let receiver:ImageReceiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createImageSource(String)

```cangjie
public func createImageSource(uri: String): ImageSource
```

**Description:** Creates an image source instance from the specified URI.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|uri|String|Yes|-|Image path, currently only supports application sandbox paths.</br>Supported formats include: .jpg .png .gif .bmp .webp RAW [SVG](#SVG-Tag-Description). |

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)|Returns an ImageSource instance.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let path: String = "../test.jpg"
    let imageSourceApi: ImageSource = createImageSource(path)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createImageSource(String, SourceOptions)

```cangjie
public func createImageSource(uri: String, options: SourceOptions): ImageSource
```

**Description:** Creates an image source instance from the specified URI.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|uri|String|Yes|-|Image path, currently only supports application sandbox paths.</br>Supported formats include: .jpg .png .gif .bmp .webp RAW [SVG](#SVG-Tag-Description).|
|options|[SourceOptions](#class-sourceoptions)|Yes|-|Image properties, including image index and default property values.|

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)|Returns an ImageSource instance.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSource: ImageSource = createImageSource("test.png", sourceOptions)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createImageSource(Int32)

```cangjie
public func createImageSource(fd: Int32): ImageSource
```

**Description:** Creates an image source instance from a file descriptor.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|fd|Int32|Yes|-|File descriptor fd.|

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)|Returns an ImageSource instance.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let imageSourceApi : ImageSource = createImageSource(0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createImageSource(Int32, SourceOptions)

```cangjie
public func createImageSource(fd: Int32, options: SourceOptions): ImageSource
```

**Description:** Creates an image source instance from a file descriptor.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|fd|Int32|Yes|-|Image file descriptor.|
|options|[SourceOptions](#class-sourceoptions)|Yes|-|Image properties, including image index and default property values.|

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)|Returns an ImageSource instance.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSource: ImageSource = createImageSource(0, sourceOptions)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createImageSource(Array\<UInt8>)

```cangjie
public func createImageSource(buf: Array<UInt8>): ImageSource
```

**Description:** Creates an image source instance from a buffer.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|buf|Array\<UInt8>|Yes|-|Image buffer array.|

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)|Returns an ImageSource instance.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let buf: Array<UInt8> = Array<UInt8>(96, repeat: 0) //96 is the required pixel buffer size, calculated as: height * width *4
    let imageSourceApi: ImageSource = createImageSource(buf)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createImageSource(Array\<UInt8>, SourceOptions)

```cangjie
public func createImageSource(buf: Array<UInt8>, options: SourceOptions): ImageSource
```

**Description:** Creates an image source instance from a buffer.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|buf|Array\<UInt8>|Yes|-|Image buffer array.|
|options|[SourceOptions](#class-sourceoptions)|Yes|-|Image properties, including image index and default property values.|

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)|Returns an ImageSource instance.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createImageSource(RawFileDescriptor, SourceOptions)

```cangjie
public func createImageSource(rawfile: RawFileDescriptor, options!: SourceOptions = SourceOptions(0)): ImageSource
```

**Description:** Creates an image source instance from the RawFileDescriptor of an image resource file.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|rawfile|[RawFileDescriptor](../LocalizationKit/cj-apis-raw_file_descriptor.md#class-rawfiledescriptor)|Yes|-|RawFileDescriptor of the image resource file.|
|options|[SourceOptions](#class-sourceoptions)|No|SourceOptions(0)| **Named parameter.** Image properties, including pixel density, pixel format, and image dimensions.|

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)|Returns an ImageSource instance.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.resource_manager.ResourceManager

let resourceManager = Global.getResourceManager() // Requires obtaining the Context application context. See Usage Instructions above.
try {
    let rawfd = resourceManager.getRawFd("test.png")
    createImageSource(rawfd)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "error code: ${e.code}, message: ${e.message}.", "")
}
```## func createPixelMap(Array\<UInt8>, InitializationOptions)

```cangjie
public func createPixelMap(colors: Array<UInt8>, options: InitializationOptions): PixelMap
```

**Function:** Creates a PixelMap with specified attributes, defaulting to BGRA_8888 format for data processing. Currently only BGRA_8888 format is supported.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| colors | Array\<UInt8> | Yes | - | Color array in BGRA_8888 format. |
| options | [InitializationOptions](#class-initializationoptions) | Yes | - | Attributes for creating the pixel, including transparency, size, thumbnail value, pixel format, and editability. |

**Return Value:**

| Type | Description |
|:----|:----|
| [PixelMap](#class-pixelmap) | Returns the PixelMap.<br>If the created pixelmap size exceeds the original image size, returns the original pixelmap size. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980104 | Failed to initialize the internal object. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let color: Array<UInt8> = Array<UInt8>(96, repeat: 0) //96 is the required pixel buffer size, calculated as: height * width *4
    let opts: InitializationOptions = InitializationOptions(Size(4, 6))
    let pixelMap = createPixelMap(color, opts)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class Component

```cangjie
public class Component {
    public let componentType: ComponentType
    public let rowStride: Int32
    public let pixelStride: Int32
    public let byteBuffer: Array<UInt8>
}
```

**Function:** Describes image color components.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### let byteBuffer

```cangjie
public let byteBuffer: Array<UInt8>
```

**Function:** Component buffer.

**Type:** Array\<UInt8>

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### let componentType

```cangjie
public let componentType: ComponentType
```

**Function:** Component type.

**Type:** [ComponentType](#enum-componenttype)

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### let pixelStride

```cangjie
public let pixelStride: Int32
```

**Function:** Pixel stride.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### let rowStride

```cangjie
public let rowStride: Int32
```

**Function:** Row stride.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

## class DecodingOptions

```cangjie
public class DecodingOptions {
    public var sampleSize: UInt32
    public var rotate: UInt32
    public var editable: Bool
    public var desiredSize: Size
    public var desiredRegion: Region
    public var desiredPixelFormat: PixelMapFormat
    public var index: UInt32
    public var fitDensity: Int32
    public var desiredColorSpace:?ColorSpaceManager
    public var desiredDynamicRange: DecodingDynamicRange
    public init(sampleSize!: UInt32 = 1, rotate!: UInt32 = 0, editable!: Bool = false,
        desiredSize!: Size = Size(0, 0), desiredRegion!: Region = Region(Size(0, 0), 0, 0),
        desiredPixelFormat!: PixelMapFormat = Unknown, index!: UInt32 = 0, fitDensity!: Int32 = 0,
        desiredColorSpace!: ?ColorSpaceManager = None, desiredDynamicRange!: DecodingDynamicRange = Sdr)
}
```

**Function:** Image decoding configuration options.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var desiredColorSpace

```cangjie
public var desiredColorSpace:?ColorSpaceManager
```

**Function:** Target color space.

**Type:** ?[ColorSpaceManager](../ArkGraphics2D/cj-apis-color_manager.md#class-colorspacemanager)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var desiredDynamicRange

```cangjie
public var desiredDynamicRange: DecodingDynamicRange
```

**Function:** Target dynamic range, default is SDR.

If the platform does not support HDR, this setting is invalid and will default to decoding SDR content.

**Type:** [DecodingDynamicRange](#enum-decodingdynamicrange)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var desiredPixelFormat

```cangjie
public var desiredPixelFormat: PixelMapFormat
```

**Function:** Decoded pixel format.

**Type:** [PixelMapFormat](#enum-pixelmapformat)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var desiredRegion

```cangjie
public var desiredRegion: Region
```

**Function:** Decoding region.

**Type:** [Region](#class-region)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var desiredSize

```cangjie
public var desiredSize: Size
```

**Function:** Desired output size.

**Type:** [Size](#class-size)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var editable

```cangjie
public var editable: Bool
```

**Function:** Editability. When set to false, the image cannot be further edited (e.g., crop operations will fail).

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var fitDensity

```cangjie
public var fitDensity: Int32
```

**Function:** Image pixel density in ppi.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var index

```cangjie
public var index: UInt32
```

**Function:** Decoding image index.

**Type:** UInt32

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var rotate

```cangjie
public var rotate: UInt32
```

**Function:** Rotation angle.

**Type:** UInt32

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var sampleSize

```cangjie
public var sampleSize: UInt32
```

**Function:** Thumbnail sampling size, currently only supports 1.

**Type:** UInt32

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### init(UInt32, UInt32, Bool, Size, Region, PixelMapFormat, UInt32, Int32, ?ColorSpaceManager, DecodingDynamicRange)

```cangjie
public init(sampleSize!: UInt32 = 1, rotate!: UInt32 = 0, editable!: Bool = false,
    desiredSize!: Size = Size(0, 0), desiredRegion!: Region = Region(Size(0, 0), 0, 0),
    desiredPixelFormat!: PixelMapFormat = Unknown, index!: UInt32 = 0, fitDensity!: Int32 = 0,
    desiredColorSpace!: ?ColorSpaceManager = None, desiredDynamicRange!: DecodingDynamicRange = Sdr)
```

**Function:** Creates a DecodingOptions object.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| sampleSize | UInt32 | No | 1 | **Named parameter.** Thumbnail sampling size, currently only supports 1. |
| rotate | UInt32 | No | 0 | **Named parameter.** Rotation angle. |
| editable | Bool | No | false | **Named parameter.** Editability. When set to false, the image cannot be further edited (e.g., crop operations will fail). |
| desiredSize | [Size](#class-size) | No | Size(0, 0) | **Named parameter.** Desired output size. |
| desiredRegion | [Region](#class-region) | No | Region(Size(0, 0), 0, 0) | **Named parameter.** Decoding region. |
| desiredPixelFormat | [PixelMapFormat](#enum-pixelmapformat) | No | Unknown | **Named parameter.** Decoded pixel format. |
| index | UInt32 | No | 0 | **Named parameter.** Decoding image index. |
| fitDensity | Int32 | No | 0 | **Named parameter.** Image pixel density in ppi. |
| desiredColorSpace | ?[ColorSpaceManager](../ArkGraphics2D/cj-apis-color_manager.md#class-colorspacemanager) | No | None | **Named parameter.** Target color space. |
| desiredDynamicRange | [DecodingDynamicRange](#enum-decodingdynamicrange) | No | Sdr | **Named parameter.** Target dynamic range.<br>If the platform does not support HDR, this setting is invalid and will default to decoding SDR content. |

## class Image

```cangjie
public class Image {}
```

**Function:** Provides basic image operations, including obtaining image information and reading/writing image data.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### prop clipRect

```cangjie
public prop clipRect: Region
```

**Function:** Image region to be cropped.

**Type:** [Region](#class-region)

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### prop format

```cangjie
public prop format: Int32
```

**Function:** Image format, refer to [PixelMapFormat](#enum-pixelmapformat).

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### prop size

```cangjie
public prop size: Size
```

**Function:** Image size.

**Type:** [Size](#class-size)

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### func getComponent(ComponentType)

```cangjie
public func getComponent(componentType: ComponentType): Component
```

**Function:** Retrieves the component buffer from the image based on the component type and returns the result.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| componentType | [ComponentType](#enum-componenttype) | Yes | - | Image component type. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Component](#class-component) | Returns the component buffer. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let size = Size(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let img = receiver.readNextImage()
    let component : Component = img.getComponent(ComponentType.Jpeg)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func release()

```cangjie
public func release(): Unit
```

**Function:** Releases the current image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let size = Size(8, 8192)
    let receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let img = receiver.readNextImage()
    img.release()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class ImageInfo

```cangjie
public class ImageInfo {
    public var size: Size
    public var density: Int32
    public var stride: Int32
    public var pixelFormat: PixelMapFormat
    public var alphaType: AlphaType
    public var mimeType: String
    public var isHdr: Bool
}
```

**Description:** Represents image information.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var alphaType

```cangjie
public var alphaType: AlphaType
```

**Description:** Alpha transparency.

**Type:** [AlphaType](#enum-alphatype)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var density

```cangjie
public var density: Int32
```

**Description:** Pixel density in ppi (pixels per inch).

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var isHdr

```cangjie
public var isHdr: Bool
```

**Description:** Indicates whether the image is High Dynamic Range (HDR). For [ImageSource](#class-imagesource), it indicates whether the source image is HDR; for [PixelMap](#class-pixelmap), it indicates whether the decoded pixelmap is HDR.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var mimeType

```cangjie
public var mimeType: String
```

**Description:** The actual image format (MIME type).

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var pixelFormat

```cangjie
public var pixelFormat: PixelMapFormat
```

**Description:** Pixel format.

**Type:** [PixelMapFormat](#enum-pixelmapformat)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var size

```cangjie
public var size: Size
```

**Description:** Image dimensions.

**Type:** [Size](#class-size)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var stride

```cangjie
public var stride: Int32
```

**Description:** Stride, the space occupied by each row of pixels in memory. stride >= region.size.width*4.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

## class ImagePacker

```cangjie
public class ImagePacker {}
```

**Description:** Image packer class for image compression and packaging. Before calling ImagePacker methods, an ImagePacker instance must be created via [createImagePacker](#func-createimagepacker). Currently supported formats: jpeg, webp, png.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

### prop supportedFormats

```cangjie
public prop supportedFormats: Array<String>
```

**Description:** Supported image packaging formats: jpeg, webp, png.

**Type:** Array\<String>

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

### func packToData(ImageSource, PackingOption)

```cangjie
public func packToData(source: ImageSource, options: PackingOption): Array<UInt8>
```

**Description:** Compresses or re-encodes an image.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| source | [ImageSource](#class-imagesource) | Yes | - | The image source to package. |
| options | [PackingOption](#class-packingoption) | Yes | - | Packaging parameters. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt8> | Returns compressed or packaged data. |

**Exceptions:**

- BusinessException: Error codes as follows, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980096 | The operation failed. Possible cause: 1.Image upload exception.2. Decoding process exception. 3. Insufficient memory. |
  | 62980101 | The image data is abnormal. |
  | 62980106 | The image data is too large. This status code is thrown when an error occurs during the process of checking size. |
  | 62980113 | Unknown image format.The image data provided is not in a recognized or supported format, or it may be corrupted. |
  | 62980119 | Failed to encode the image. |
  | 62980120 | Add pixelmap out of range. |
  | 62980172 | Failed to encode icc. |
  | 62980252 | Failed to create surface. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSource: ImageSource = createImageSource(data, sourceOptions)  // Replace with correct image source as per usage instructions.
    var imagePacker = createImagePacker()
    let supportedFormats = imagePacker.supportedFormats
    let packingOption = PackingOption("image/jpeg", 98)
    let packRes = imagePacker.packToData(imageSource, packingOption)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func packToData(PixelMap, PackingOption)

```cangjie
public func packToData(source: PixelMap, options: PackingOption): Array<UInt8>
```

**Description:** Compresses or re-encodes an image.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| source | [PixelMap](#class-pixelmap) | Yes | - | The image source to package. |
| options | [PackingOption](#class-packingoption) | Yes | - | Packaging parameters. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt8> | Returns compressed or packaged data. |

**Exceptions:**

- BusinessException: Error codes as follows, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980096 | The operation failed. Possible cause: 1.Image upload exception.2. Decoding process exception. 3. Insufficient memory. |
  | 62980101 | The image data is abnormal. |
  | 62980106 | The image data is too large. This status code is thrown when an error occurs during the process of checking size. |
  | 62980113 | Unknown image format.The image data provided is not in a recognized or supported format, or it may be corrupted. |
  | 62980119 | Failed to encode the image. |
  | 62980120 | Add pixelmap out of range. |
  | 62980172 | Failed to encode icc. |
  | 62980252 | Failed to create surface. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var colors: Array<UInt8> = [80, 2, 4, 8, 40, 2, 4, 8]
    var pm = createPixelMap(colors,
        InitializationOptions(Size(2, 1), scaleMode: ScaleMode.CenterCrop))
    var imagePacker = createImagePacker()
    let supportedFormats = imagePacker.supportedFormats
    let packingOption = PackingOption("image/jpeg", 98)
    let packRes = imagePacker.packToData(pm, packingOption)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func packToFile(ImageSource, Int32, PackingOption)

```cangjie
public func packToFile(source: ImageSource, fd: Int32, options: PackingOption): Unit
```

**Description:** Encodes an image directly into a file with specified parameters.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| source | [ImageSource](#class-imagesource) | Yes | - | The image source to encode. |
| fd | Int32 | Yes | - | File descriptor. |
| options | [PackingOption](#class-packingoption) | Yes | - | Packaging parameters. |

**Exceptions:**

- BusinessException: Error codes as follows, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980096 | The operation failed. Possible cause: 1.Image upload exception.2. Decoding process exception. 3. Insufficient memory. |
  | 62980101 | The image data is abnormal. |
  | 62980106 | The image data is too large. This status code is thrown when an error occurs during the process of checking size. |
  | 62980113 | Unknown image format.The image data provided is not in a recognized or supported format, or it may be corrupted. |
  | 62980115 | Invalid input parameter. |
  | 62980119 | Failed to encode the image. |
  | 62980120 | Add pixelmap out of range. |
  | 62980172 | Failed to encode icc. |
  | 62980252 | Failed to create surface. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import kit.CoreFileKit.{FileIo, OpenMode}
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSource: ImageSource = createImageSource(data, sourceOptions)  // Replace with correct image source as per usage instructions.
    var fd: Int32 = 0
    let filePath = "data/storage/el1/base/xxx.txt"
    let file = FileIo.open(filePath,mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    let packingOption = PackingOption("image/jpeg", 98)
    let imagePacker = createImagePacker()
    imagePacker.packToFile(imageSource, fd, packingOption)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func packToFile(PixelMap, Int32, PackingOption)

```cangjie
public func packToFile(source: PixelMap, fd: Int32, options: PackingOption): Unit
```

**Description:** Encodes an image directly into a file with specified parameters.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| source | [PixelMap](#class-pixelmap) | Yes | - | The image source to encode. |
| fd | Int32 | Yes | - | File descriptor. |
| options | [PackingOption](#class-packingoption) | Yes | - | Packaging parameters. |

**Exceptions:**

- BusinessException: Error codes as follows, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980096 | The operation failed. Possible cause: 1.Image upload exception.2. Decoding process exception. 3. Insufficient memory. |
  | 62980101 | The image data is abnormal. |
  | 62980106 | The image data is too large. This status code is thrown when an error occurs during the process of checking size. |
  | 62980113 | Unknown image format.The image data provided is not in a recognized or supported format, or it may be corrupted. |
  | 62980115 | Invalid input parameter. |
  | 62980119 | Failed to encode the image. |
  | 62980120 | Add pixelmap out of range. |
  | 62980172 | Failed to encode icc. |
  | 62980252 | Failed to create surface. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import kit.CoreFileKit.{FileIo, OpenMode}
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let color: Array<UInt8> = Array<UInt8>(96, repeat: 0) //96 is the required pixel buffer size, calculated as: height * width *4
    let opts: InitializationOptions = InitializationOptions(
        Size(4, 6),
        editable: true,
        pixelFormat: PixelMapFormat.Rgba8888)
    let pixelMap = createPixelMap(color, opts)
    var fd: Int32 = 0
    let filePath = "data/storage/el1/base/xxx.txt"
    let file = FileIo.open(filePath,mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    let packingOption = PackingOption("image/jpeg", 98)
    let imagePacker = createImagePacker()
    imagePacker.packToFile(pixelMap, fd, packingOption)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func release()

```cangjie
public func release(): Unit
```

**Description:** Releases the image packer instance.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let imagePacker = createImagePacker()
    imagePacker.release()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class ImagePropertyOptions

```cangjie
public class ImagePropertyOptions {
    public var index: UInt32
    public var defaultValue: String
    public init(index!: UInt32 = 0, defaultValue!: String = "")
}
```

**Description:** Represents the index for querying image properties.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var defaultValue

```cangjie
public var defaultValue: String
```

**Description:** Default property value.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### var index

```cangjie
public var index: UInt32
```

**Description:** Image sequence number.

**Type:** UInt32

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### init(UInt32, String)

```cangjie
public init(index!: UInt32 = 0, defaultValue!: String = "")
```

**Description:** Creates an ImagePropertyOptions object.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| index | UInt32 | No | 0 | **Named parameter.** Image sequence number. |
| defaultValue | String | No | "" | **Named parameter.** Default property value. |

## class ImageReceiver

```cangjie
public class ImageReceiver {}
```

**Description:** Image receiver class, used to obtain component surface ID, receive the latest image, read the next image, and release the ImageReceiver instance.

An ImageReceiver instance must be created before calling the following methods.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

### prop capacity

```cangjie
public prop capacity: Int32
```

**Description:** Number of images that can be accessed simultaneously.

**Type:** Int32

**Read/Write:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

### prop format

```cangjie
public prop format: ImageFormat
```

**Description:** Image format.

**Type:** [ImageFormat](#enum-imageformat)

**Read/Write:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

### prop size

```cangjie
public prop size: Size
```

**Description:** Image size.

**Type:** [Size](#class-size)

**Read/Write:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

### func getReceivingSurfaceId()

```cangjie
public func getReceivingSurfaceId(): String
```

**Description:** Used to obtain a surface ID for Camera or other components.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the surface ID. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let size = Size(8, 8192)
    var receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    let id: String = receiver.getReceivingSurfaceId()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func release()

```cangjie
public func release(): Unit
```

**Description:** Releases the current image receiver instance.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let size = Size(8, 8192)
    var receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
    receiver.release()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readLatestImage()

```cangjie
public func readLatestImage(): Image
```

**Description:** Reads the latest image from ImageReceiver.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Image](#class-image) | Returns an Image instance. |

### func readNextImage()

```cangjie
public func readNextImage(): Image
```

**Description:** Reads the next image from ImageReceiver.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Image](#class-image) | Returns an Image instance. |

### func on(ReceiveType, Callback0Argument)

```cangjie
public func on(eventType: ReceiveType, callback: Callback0Argument): Unit
```

**Description:** Registers a callback when receiving an image.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [ReceiveType](#enum-receivetype) | Yes | - | Type of the registered event. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function object. |

### func off(ReceiveType)

```cangjie
public func off(eventType: ReceiveType): Unit
```

**Description:** Removes the registered callback when releasing the buffer.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [ReceiveType](#enum-receivetype) | Yes | - | Type of the registered event. |

## class ImageSource

```cangjie
public class ImageSource {}
```

**Description:** Image source class, used to obtain image-related information. Before calling ImageSource methods, an ImageSource instance must be created via createImageSource.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### prop supportedFormats

```cangjie
public prop supportedFormats: Array<String>
```

**Description:** Supported image formats, including: png, jpeg, bmp, gif, webp, RAW.

**Type:** Array\<String>

**Read/Write:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

### func createPixelMap(DecodingOptions)

```cangjie
public func createPixelMap(options!: DecodingOptions = DecodingOptions()): PixelMap
```

**Description:** Creates a PixelMap object with image decoding parameters.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| options | [DecodingOptions](#class-decodingoptions) | No | DecodingOptions() | **Named parameter.** Decoding parameters. |

**Return Value:**

| Type | Description |
|:----|:----|
| [PixelMap](#class-pixelmap) | Returns a PixelMap instance. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source as per usage instructions.
    let option = DecodingOptions(
        sampleSize: 1,
        rotate: 10,
        editable: true,
        desiredSize: Size(3, 4),
        desiredRegion: Region(Size(3, 4), 0, 0),
        desiredPixelFormat: PixelMapFormat.Rgba8888,
        index: 0,
        fitDensity: 20
    )
    let pixelMap = imageSourceApi.createPixelMap(options: option)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func createPixelMapList(DecodingOptions)

```cangjie
public func createPixelMapList(options!: DecodingOptions = DecodingOptions()): Array<PixelMap>
```

**Description:** Creates an array of PixelMap objects with image decoding parameters.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| options | [DecodingOptions](#class-decodingoptions) | No | DecodingOptions() | **Named parameter.** Decoding parameters. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[PixelMap](#class-pixelmap)> | Returns an array of PixelMap objects. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980096 | The operation failed. Possible cause: 1.Image upload exception.2. Decoding process exception. 3. Insufficient memory. |
  | 62980099 | The shared memory data is abnormal. |
  | 62980101 | The image data is abnormal. |
  | 62980103 | The image data is not supported. |
  | 62980106 | The image data is too large. This status code is thrown when an error occurs during the process of checking size. |
  | 62980109 | Failed to crop the image. |
  | 62980111 | The image source data is incomplete. |
  | 62980115 | Invalid image parameter. |
  | 62980116 | Failed to decode the image. |
  | 62980118 | Failed to create the image plugin. |
  | 62980137 | Invalid media operation. |
  | 62980173 | The DMA memory does not exist. |
  | 62980174 | The DMA memory data is abnormal. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source as per usage instructions.
    let option = DecodingOptions(
        sampleSize: 1,
        rotate: 10,
        editable: true,
        desiredSize: Size(3, 4),
        desiredRegion: Region(Size(3, 4), 0, 0),
        desiredPixelFormat: PixelMapFormat.Rgba8888,
        index: 0,
        fitDensity: 20
    )
    let pixelMap = imageSourceApi.createPixelMapList(options: option)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func getDelayTimeList()

```cangjie
public func getDelayTimeList(): Array<Int32>
```

**Function:** Retrieves the array of image delay times. This interface is only applicable to GIF images.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

**Return Value:**

| Type          | Description                     |
| ------------- | ------------------------------- |
| Array\<Int32> | Returns the array of delay times. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | ------------- | ------------- |
  | 62980096      | The operation failed. Possible causes: 1. Image upload exception. 2. Decoding process exception. 3. Insufficient memory. |
  | 62980110      | The image source data is incorrect. |
  | 62980111      | The image source data is incomplete. |
  | 62980115      | Invalid image parameter. |
  | 62980116      | Failed to decode the image. |
  | 62980118      | Failed to create the image plugin. |
  | 62980122      | Failed to decode the image header. |
  | 62980149      | Invalid MIME type for the image source. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let list = imageSourceApi.getDelayTimeList()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getFrameCount()

```cangjie
public func getFrameCount(): UInt32
```

**Function:** Retrieves the number of image frames.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

**Return Value:**

| Type   | Description               |
| ------ | ------------------------- |
| UInt32 | Returns the number of image frames. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | ------------- | ------------- |
  | 62980096      | The operation failed. Possible causes: 1. Image upload exception. 2. Decoding process exception. 3. Insufficient memory. |
  | 62980111      | The image source data is incomplete. |
  | 62980112      | The image format does not match. |
  | 62980113      | Unknown image format. The image data provided is not in a recognized or supported format, or it may be corrupted. |
  | 62980115      | Invalid image parameter. |
  | 62980116      | Failed to decode the image. |
  | 62980118      | Failed to create the image plugin. |
  | 62980122      | Failed to decode the image header. |
  | 62980137      | Invalid media operation. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let count = imageSourceApi.getFrameCount()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getImageInfo(UInt32)

```cangjie
public func getImageInfo(index!: UInt32 = 0): ImageInfo
```

**Function:** Retrieves image information.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

**Parameters:**

| Parameter | Type  | Required | Default | Description |
| --------- | ----- | -------- | ------- | ----------- |
| index     | UInt32 | No       | 0       | **Named parameter.** The sequence number when creating the image source. Defaults to 0 if not specified. |

**Return Value:**

| Type                     | Description                     |
| ------------------------ | ------------------------------- |
| [ImageInfo](#class-imageinfo) | Returns the retrieved image information. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    imageSourceApi.getImageInfo(index : 0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getImageProperty(PropertyKey, ImagePropertyOptions)

```cangjie
public func getImageProperty(key: PropertyKey, options!: ImagePropertyOptions = ImagePropertyOptions()): String
```

**Function:** Retrieves the value of the specified property key for the image at the given index. Only supports JPEG files with EXIF information.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

**Parameters:**

| Parameter | Type                                | Required | Default               | Description |
| --------- | ----------------------------------- | -------- | --------------------- | ----------- |
| key       | [PropertyKey](#enum-propertykey)    | Yes      | -                     | The image property name. |
| options   | [ImagePropertyOptions](#class-imagepropertyoptions) | No       | ImagePropertyOptions() | **Named parameter.** Image properties, including the image sequence number and default property value. |

**Return Value:**

| Type   | Description                                     |
| ------ | ----------------------------------------------- |
| String | Returns the image property value. If retrieval fails, returns the default property value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | ------------- | ------------- |
  | 62980096      | The operation failed. Possible causes: 1. Image upload exception. 2. Decoding process exception. 3. Insufficient memory. |
  | 62980103      | The image data is not supported. |
  | 62980110      | The image source data is incorrect. |
  | 62980111      | The image source data is incomplete. |
  | 62980112      | The image format does not match. |
  | 62980113      | Unknown image format. The image data provided is not in a recognized or supported format, or it may be corrupted. |
  | 62980115      | Invalid image parameter. |
  | 62980118      | Failed to create the image plugin. |
  | 62980122      | Failed to decode the image header. |
  | 62980123      | The image does not support EXIF decoding. |
  | 62980135      | The EXIF value is invalid. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    imageSourceApi.getImageProperty(PropertyKey.ImageLength)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func modifyImageProperty(PropertyKey, String)

```cangjie
public func modifyImageProperty(key: PropertyKey, value: String): Unit
```

**Function:** Modifies the value of the specified image property key. Only supports JPEG files with EXIF information.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

**Parameters:**

| Parameter | Type                             | Required | Default | Description |
| --------- | -------------------------------- | -------- | ------- | ----------- |
| key       | [PropertyKey](#enum-propertykey) | Yes      | -       | The image property name. |
| value     | String                           | Yes      | -       | The property value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | ------------- | ------------- |
  | 62980104      | Failed to initialize the internal object. |
  | 62980110      | The image source data is incorrect. |
  | 62980115      | Invalid image parameter. |
  | 62980123      | The image does not support EXIF decoding. |
  | 62980133      | The EXIF data is out of range. |
  | 62980135      | The EXIF value is invalid. |
  | 62980146      | The EXIF data failed to be written to the file. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    imageSourceApi.modifyImageProperty(PropertyKey.ImageLength, "200")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func release()

```cangjie
public func release(): Unit
```

**Function:** Releases the image source instance.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    imageSourceApi.release()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func updateData(Array\<UInt8>, Bool, UInt32, UInt32)

```cangjie
public func updateData(buf: Array<UInt8>, isFinished: Bool, offset: UInt32, length: UInt32): Unit
```

**Function:** Updates incremental data, used in conjunction with CreateIncrementalSource.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 22

**Parameters:**

| Parameter  | Type          | Required | Default | Description |
| ---------- | ------------- | -------- | ------- | ----------- |
| buf        | Array\<UInt8> | Yes      | -       | Incremental data. |
| isFinished | Bool          | Yes      | -       | Whether the update is complete. |
| offset     | UInt32        | Yes      | -       | Offset. |
| length     | UInt32        | Yes      | -       | Array length. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let testPng = Array<UInt8>(16500, repeat: 0)
    let bufferSize = 5000
    var offset = 0
    var isFinished = false
    while (offset < testPng.size) {
        var oneStep = testPng.slice(offset, min(bufferSize, testPng.size - offset))
        if (oneStep.size < bufferSize) {
            isFinished = true
        }
        imageSourceApi.updateData(oneStep, isFinished, 0, UInt32(oneStep.size))
        offset = offset + oneStep.size
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class InitializationOptions

```cangjie
public class InitializationOptions {
    public var alphaType: AlphaType
    public var editable: Bool
    public var srcPixelFormat: PixelMapFormat
    public var pixelFormat: PixelMapFormat
    public var scaleMode: ScaleMode
    public var size: Size
    public init(size: Size, alphaType!: AlphaType = AlphaType.Premul, editable!: Bool = false, srcPixelFormat!: PixelMapFormat = PixelMapFormat.Bgra8888,
        pixelFormat!: PixelMapFormat = PixelMapFormat.Bgra8888, scaleMode!: ScaleMode = ScaleMode.FitTargetSize)
}
```

**Function:** Initialization options for PixelMap.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var alphaType

```cangjie
public var alphaType: AlphaType
```

**Function:** Transparency.

**Type:** [AlphaType](#enum-alphatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var editable

```cangjie
public var editable: Bool
```

**Function:** Whether it is editable.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var pixelFormat

```cangjie
public var pixelFormat: PixelMapFormat
```

**Function:** Pixel format.

**Type:** [PixelMapFormat](#enum-pixelmapformat)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var scaleMode

```cangjie
public var scaleMode: ScaleMode
```

**Function:** Scaling mode.

**Type:** [ScaleMode](#enum-scalemode)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var size

```cangjie
public var size: Size
```

**Function:** Image creation size.

**Type:** [Size](#class-size)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var srcPixelFormat

```cangjie
public var srcPixelFormat: PixelMapFormat
```

**Function:** The pixel format of the input buffer data. Default is BGRA_8888.

**Type:** [PixelMapFormat](#enum-pixelmapformat)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### init(Size, AlphaType, Bool, PixelMapFormat, PixelMapFormat, ScaleMode)

```cangjie
public init(size: Size, alphaType!: AlphaType = AlphaType.Premul, editable!: Bool = false, srcPixelFormat!: PixelMapFormat = PixelMapFormat.Bgra8888,
    pixelFormat!: PixelMapFormat = PixelMapFormat.Bgra8888, scaleMode!: ScaleMode = ScaleMode.FitTargetSize)
```

**Function:** Creates an InitializationOptions object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

| Parameter      | Type                          | Required | Default                  | Description |
| -------------- | ----------------------------- | -------- | ------------------------ | ----------- |
| size           | [Size](#class-size)           | Yes      | -                        | **Named parameter.** Image creation size. |
| alphaType      | [AlphaType](#enum-alphatype)  | No       | AlphaType.Premul         | **Named parameter.** Transparency. |
| editable       | Bool                          | No       | false                    | **Named parameter.** Whether it is editable. |
| srcPixelFormat | [PixelMapFormat](#enum-pixelmapformat) | No       | PixelMapFormat.Bgra8888  | **Named parameter.** The pixel format of the input buffer data. |
| pixelFormat    | [PixelMapFormat](#enum-pixelmapformat) | No       | PixelMapFormat.Bgra8888  | **Named parameter.** Pixel format. |
| scaleMode      | [ScaleMode](#enum-scalemode)  | No       | ScaleMode.FitTargetSize  | **Named parameter.** Scaling mode. |## class PackingOption

```cangjie
public class PackingOption {
    public var format: String
    public var quality: UInt8
    public var bufferSize: UInt64
    public var desiredDynamicRange: PackingDynamicRange
    public var needsPackProperties: Bool
    public init(format: String, quality: UInt8, bufferSize!: UInt64 = 25  * 1024  * 1024,
        desiredDynamicRange!: PackingDynamicRange = Sdr, needsPackProperties!: Bool = false)
}
```

**Function:** Represents image packing options.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

### var bufferSize

```cangjie
public var bufferSize: UInt64
```

**Function:** Size of the buffer for receiving encoded data, in bytes. Defaults to 25MB if not specified. If the encoded image exceeds 25MB, this size must be specified. bufferSize must be larger than the size of the encoded image. This parameter does not apply when using [packToFile](#func-packtofileimagesource-int32-packingoption).

**Type:** UInt64

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

### var desiredDynamicRange

```cangjie
public var desiredDynamicRange: PackingDynamicRange
```

**Function:** Target dynamic range. Default value is SDR.

**Type:** [PackingDynamicRange](#enum-packingdynamicrange)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

### var format

```cangjie
public var format: String
```

**Function:** Target format.</br>Currently supports "image/jpeg", "image/webp", "image/png", and "image/heif" (availability varies by hardware device).

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

### var needsPackProperties

```cangjie
public var needsPackProperties: Bool
```

**Function:** Whether to encode image property information, such as EXIF. Default value is false.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

### var quality

```cangjie
public var quality: UInt8
```

**Function:** Parameter for setting output image quality in JPEG encoding, ranging from 0-100. 0 represents the lowest quality, 100 represents the highest quality. Higher quality results in larger image file sizes.

**Type:** UInt8

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

### init(String, UInt8, UInt64, PackingDynamicRange, Bool)

```cangjie
public init(format: String, quality: UInt8, bufferSize!: UInt64 = 0,
    desiredDynamicRange!: PackingDynamicRange = Sdr, needsPackProperties!: Bool = false)
```

**Function:** Creates a PackingOption object.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| format | String | Yes | - | Target format.</br>Currently supports "image/jpeg", "image/webp", "image/png", and "image/heif" (availability varies by hardware device). |
| quality | UInt8 | Yes | - | Parameter for setting output image quality in JPEG encoding, ranging from 0-100. 0 represents the lowest quality, 100 represents the highest quality. Higher quality results in larger image file sizes. |
| bufferSize | UInt64 | No | 0 | **Named parameter.** Size of the buffer for receiving encoded data, in bytes. Defaults to 25MB if not specified. If the encoded image exceeds 25MB, this size must be specified. bufferSize must be larger than the size of the encoded image. This parameter does not apply when using [packToFile](#func-packtofileimagesource-int32-packingoption). |
| desiredDynamicRange | [PackingDynamicRange](#enum-packingdynamicrange) | No | Sdr | **Named parameter.** Target dynamic range. |
| needsPackProperties | Bool | No | false | **Named parameter.** Whether to encode image property information, such as EXIF. |

## class PixelMap

```cangjie
public class PixelMap {}
```

**Function:** Image pixel class for reading or writing image data and obtaining image information. Before calling PixelMap methods, a PixelMap instance must be created via [createPixelMap](#func-createpixelmaparrayuint8-initializationoptions). Currently, the maximum serialized size of pixelmap is 128MB; exceeding this limit will cause display failure. Size is calculated as (width * height * bytes per pixel).

PixelMap supports cross-thread calls via Worker. After PixelMap is transferred across threads via Worker, all interfaces of the original PixelMap cannot be called; otherwise, error 501 (server does not support the requested functionality) will occur.

Before calling PixelMap methods, a PixelMap object must be created via [createPixelMap](#func-createpixelmaparrayuint8-initializationoptions).

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### prop isEditable

```cangjie
public prop isEditable: Bool
```

**Function:** Sets whether the image pixels can be edited.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### prop isStrideAlignment

```cangjie
public prop isStrideAlignment: Bool
```

**Function:** Sets whether the image memory is DMA memory.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### func applyColorSpace(ColorSpaceManager)

```cangjie
public func applyColorSpace(targetColorSpace: ColorSpaceManager): Unit
```

**Function:** Performs color space conversion on image pixels based on the input target color space.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| targetColorSpace | [ColorSpaceManager](../ArkGraphics2D/cj-apis-color_manager.md#class-colorspacemanager) | Yes | - | Target color space, supports Srgb, DCI_P3, DisplayP3, ADOBE_RGB_1998. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980104 | Failed to initialize the internal object. |
  | 62980108 | Failed to convert the color space. |
  | 62980115 | Invalid image parameter. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import kit.ArkGraphics2D.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with correct image source, refer to usage instructions.
    let pixelMap = imageSourceApi.createPixelMap()
    let colorSpaceManager = create(Srgb)
    pixelMap.applyColorSpace(colorSpaceManager)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func createAlphaPixelmap()

```cangjie
public func createAlphaPixelmap(): PixelMap
```

**Function:** Generates a pixelmap containing only alpha channel information based on the alpha channel, which can be used for shadow effects.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [PixelMap](#class-pixelmap) | Returns a pixelmap instance. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with correct image source, refer to usage instructions.
    let pixelMap = imageSourceApi.createPixelMap()
    let alphaPixelmap = pixelMap.createAlphaPixelmap()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func crop(Region)

```cangjie
public func crop(region: Region): Unit
```

**Function:** Crops the image based on the input dimensions.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| region | [Region](#class-region) | Yes | - | Dimensions for cropping. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with correct image source, refer to usage instructions.
    let pixelMap = imageSourceApi.createPixelMap()
    let region: Region = Region(Size(100, 100), 0, 0)
    pixelMap.crop(region)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func flip(Bool, Bool)

```cangjie
public func flip(horizontal: Bool, vertical: Bool): Unit
```

**Function:** Flips the image based on the input conditions.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| horizontal | Bool | Yes | - | Horizontal flip. |
| vertical | Bool | Yes | - | Vertical flip. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with correct image source, refer to usage instructions.
    let pixelMap = imageSourceApi.createPixelMap()
    let horizontal: Bool = true
    let vertical: Bool = false
    pixelMap.flip(horizontal, vertical)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getBytesNumberPerRow()

```cangjie
public func getBytesNumberPerRow(): UInt32
```

**Function:** Gets the number of bytes per row of image pixels.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Number of bytes per row of image pixels. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with correct image source, refer to usage instructions.
    let pixelMap = imageSourceApi.createPixelMap()
    let rowCount : UInt32 = pixelMap.getBytesNumberPerRow()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getColorSpace()

```cangjie
public func getColorSpace(): ColorSpaceManager
```

**Function:** Gets the wide color gamut information of the image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [ColorSpaceManager](../ArkGraphics2D/cj-apis-color_manager.md#class-colorspacemanager) | Wide color gamut information of the image. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980101 | If the image data abnormal. |
  | 62980103 | If the image data unsupport. |
  | 62980115 | If the image parameter invalid. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import kit.ArkGraphics2D.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with correct image source, refer to usage instructions.
    let pixelMap = imageSourceApi.createPixelMap()
    let colorSpaceManager = pixelMap.getColorSpace()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func getDensity()

```cangjie
public func getDensity(): Int32
```

**Function:** Gets the pixel density of the current image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Int32|The pixel density of the image.|

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    let getDensity : Int32 = pixelMap.getDensity()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getImageInfo()

```cangjie
public func getImageInfo(): ImageInfo
```

**Function:** Gets the pixel information of the image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[ImageInfo](#class-imageinfo)|Used to obtain the pixel information of the image. Returns an error message if the operation fails.|

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    pixelMap.getImageInfo()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getPixelBytesNumber()

```cangjie
public func getPixelBytesNumber(): UInt32
```

**Function:** Gets the total number of bytes of the image pixels.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|UInt32|The total number of bytes of the image pixels.|

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    let pixelBytesNumber : UInt32 = pixelMap.getPixelBytesNumber()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func opacity(Float32)

```cangjie
public func opacity(rate: Float32): Unit
```

**Function:** Sets the transparency ratio to achieve the corresponding transparency effect for the PixelMap.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|rate|Float32|Yes|-|The value of the transparency ratio.|

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    let rate: Float32 = 0.5
    pixelMap.opacity(rate)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readPixels(PositionArea)

```cangjie
public func readPixels(area: PositionArea): Unit
```

**Function:** Reads the image data within the specified area.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|area|[PositionArea](#class-positionarea)|Yes|-|The area size. The data is read based on the area.|

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    let area: PositionArea = PositionArea(
        Array<UInt8>(8, repeat: 0),
        0,
        8,
        Region(Size(1, 2), 0, 0)
    )
    pixelMap.readPixels(area)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readPixelsToBuffer(Array\<UInt8>)

```cangjie
public func readPixelsToBuffer(dst: Array<UInt8>): Unit
```

**Function:** Reads the image pixel data and writes the result into an Array\<UInt8>. If the PixelMap is created in BGRA_8888 format, the read pixel data will be consistent with the original data.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|dst|Array\<UInt8>|Yes|-|The buffer to which the image pixel data is written after the function is executed. The buffer size can be obtained using the [getPixelBytesNumber](#func-getpixelbytesnumber) interface.|

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    let readBuffer: Array<UInt8> = Array<UInt8>(96, repeat: 0) //96 is the size of the pixel buffer to be created, calculated as: height * width *4
    pixelMap.readPixelsToBuffer(readBuffer)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func release()

```cangjie
public func release(): Unit
```

**Function:** Releases the PixelMap object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    pixelMap.release()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func rotate(Float32)

```cangjie
public func rotate(angle: Float32): Unit
```

**Function:** Rotates the image by the specified angle.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|angle|Float32|Yes|-|The rotation angle of the image.|

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    let angle: Float32 = 90.0
    pixelMap.rotate(angle)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func scale(Float32, Float32)

```cangjie
public func scale(x: Float32, y: Float32): Unit
```

**Function:** Scales the image based on the specified width and height.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|x|Float32|Yes|-|The scaling factor for the width.|
|y|Float32|Yes|-|The scaling factor for the height.|

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    pixelMap.scale(1.0, 1.0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setColorSpace(ColorSpaceManager)

```cangjie
public func setColorSpace(colorSpace: ColorSpaceManager): Unit
```

**Function:** Sets the wide color gamut information of the image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|colorSpace|[ColorSpaceManager](../ArkGraphics2D/cj-apis-color_manager.md#class-colorspacemanager)|Yes|-|The wide color gamut information of the image.|

**Exceptions:**

- BusinessException: The error codes are as follows. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980111 | The image source data is incomplete. |
  | 62980115 | If the image parameter invalid. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import kit.ArkGraphics2D.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    let colorSpaceManager = create(Srgb)
    pixelMap.setColorSpace(colorSpaceManager)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func translate(Float32, Float32)

```cangjie
public func translate(x: Float32, y: Float32): Unit
```

**Function:** Translates the image based on the specified coordinates.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|x|Float32|Yes|-|The x-coordinate of the area.|
|y|Float32|Yes|-|The y-coordinate of the area.|

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    let translateX: Float32 = 50.0
    let translateY: Float32 = 10.0
    pixelMap.translate(translateX, translateY)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeBufferToPixels(Array\<UInt8>)

```cangjie
public func writeBufferToPixels(src: Array<UInt8>): Unit
```

**Function:** Reads the image data from the buffer and writes the result into the PixelMap.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|src|Array\<UInt8>|Yes|-|The image pixel data.|

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    let color: Array<UInt8> = Array<UInt8>(96, {i => UInt8(i)}) //96 is the size of the pixel buffer to be created, calculated as: height * width *4
    pixelMap.writeBufferToPixels(color)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writePixels(PositionArea)

```cangjie
public func writePixels(area: PositionArea): Unit
```

**Function:** Writes the PixelMap into the specified area.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|area|[PositionArea](#class-positionarea)|Yes|-|The area into which the PixelMap is written.|

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
    let sourceOptions: SourceOptions = SourceOptions(120)
    let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
    let pixelMap = imageSourceApi.createPixelMap()
    let area: PositionArea = PositionArea(
        Array<UInt8>(8, {i => UInt8(i)}),
        0,
        8,
        Region(Size(1, 2), 0, 0)
    )
    pixelMap.writePixels(area)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
``````markdown
## class PositionArea

```cangjie
public class PositionArea {
    public var pixels: Array<UInt8>
    public var offset: UInt32
    public var stride: UInt32
    public var region: Region
    public init(pixels: Array<UInt8>, offset: UInt32, stride: UInt32, region: Region)
}
```

**Function:** Represents data within a specified region of an image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var offset

```cangjie
public var offset: UInt32
```

**Function:** Offset value.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var pixels

```cangjie
public var pixels: Array<UInt8>
```

**Function:** Pixels.

**Type:** Array\<UInt8>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var region

```cangjie
public var region: Region
```

**Function:** Region for read/write operations. The sum of the region width and X-coordinate must not exceed the original image width, and the sum of the region height and Y-coordinate must not exceed the original image height.

**Type:** [Region](#class-region)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var stride

```cangjie
public var stride: UInt32
```

**Function:** Stride, the space occupied by each row of pixels in memory. stride >= region.size.width*4.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### init(Array\<UInt8>, UInt32, UInt32, Region)

```cangjie
public init(pixels: Array<UInt8>, offset: UInt32, stride: UInt32, region: Region)
```

**Function:** Creates a PositionArea object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| pixels | Array\<UInt8> | Yes | - | Pixels. |
| offset | UInt32 | Yes | - | Offset value. |
| stride | UInt32 | Yes | - | Stride, the space occupied by each row of pixels in memory. stride >= region.size.width*4. |
| region | [Region](#class-region) | Yes | - | Region for read/write operations. The sum of the region width and X-coordinate must not exceed the original image width, and the sum of the region height and Y-coordinate must not exceed the original image height. |

## class Region

```cangjie
public class Region {
    public var size: Size
    public var x: Int32
    public var y: Int32
    public init(size: Size, x: Int32, y: Int32)
}
```

**Function:** Represents region information.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var size

```cangjie
public var size: Size
```

**Function:** Region size.

**Type:** [Size](#class-size)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var x

```cangjie
public var x: Int32
```

**Function:** X-coordinate of the region.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var y

```cangjie
public var y: Int32
```

**Function:** Y-coordinate of the region.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### init(Size, Int32, Int32)

```cangjie
public init(size: Size, x: Int32, y: Int32)
```

**Function:** Creates a Region object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Size](#class-size) | Yes | - | Region size. |
| x | Int32 | Yes | - | X-coordinate of the region. |
| y | Int32 | Yes | - | Y-coordinate of the region. |

## class Size

```cangjie
public class Size {
    public var height: Int32
    public var width: Int32
    public init(height: Int32, width: Int32)
}
```

**Function:** Represents image dimensions.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var height

```cangjie
public var height: Int32
```

**Function:** Height of the output image.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var width

```cangjie
public var width: Int32
```

**Function:** Width of the output image.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### init(Int32, Int32)

```cangjie
public init(height: Int32, width: Int32)
```

**Function:** Creates a Size object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| height | Int32 | Yes | - | Height of the output image. |
| width | Int32 | Yes | - | Width of the output image. |

## class SourceOptions

```cangjie
public class SourceOptions {
    public var sourceDensity: Int32
    public var sourcePixelFormat: PixelMapFormat
    public var sourceSize: Size
    public init(sourceDensity: Int32, sourcePixelFormat!: PixelMapFormat = PixelMapFormat.Unknown, sourceSize!: Size = Size(0, 0))
}
```

**Function:** Initialization options for ImageSource.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var sourceDensity

```cangjie
public var sourceDensity: Int32
```

**Function:** Pixel density of the image resource, in DPI.

When the desiredSize parameter in [DecodingOptions](#class-decodingoptions) is not set, and both SourceOptions.sourceDensity and DecodingOptions.fitDensity are non-zero, the decoded output pixelmap will be scaled.

The scaled width is calculated as follows (height is similar): (width * fitDensity + (sourceDensity >> 1)) / sourceDensity.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var sourcePixelFormat

```cangjie
public var sourcePixelFormat: PixelMapFormat
```

**Function:** Pixel format of the image, default is UNKNOWN.

**Type:** [PixelMapFormat](#enum-pixelmapformat)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### var sourceSize

```cangjie
public var sourceSize: Size
```

**Function:** Pixel size of the image, default is empty.

**Type:** [Size](#class-size)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### init(Int32, PixelMapFormat, Size)

```cangjie
public init(sourceDensity: Int32, sourcePixelFormat!: PixelMapFormat = PixelMapFormat.Unknown, sourceSize!: Size = Size(0, 0))
```

**Function:** Creates a SourceOptions object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| sourceDensity | Int32 | Yes | - | Pixel density of the image resource, in DPI.<br>When the desiredSize parameter in [DecodingOptions](#class-decodingoptions) is not set, and both SourceOptions.sourceDensity and DecodingOptions.fitDensity are non-zero, the decoded output pixelmap will be scaled.<br>The scaled width is calculated as follows (height is similar): (width * fitDensity + (sourceDensity >> 1)) / sourceDensity. |
| sourcePixelFormat | [PixelMapFormat](#enum-pixelmapformat) | No | PixelMapFormat.Unknown | **Named parameter.** Pixel format of the image, default is UNKNOWN. |
| sourceSize | [Size](#class-size) | No | Size(0, 0) | **Named parameter.** Pixel size of the image, default is empty. |

## enum AlphaType

```cangjie
public enum AlphaType <: Equatable<AlphaType> & ToString {
    | Unknown
    | Opaque
    | Premul
    | UnPremul
    | ...
}
```

**Function:** Transparency type of an image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parent Types:**

- Equatable\<AlphaType>
- ToString

### Opaque

```cangjie
Opaque
```

**Function:** No alpha or the image is opaque.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Premul

```cangjie
Premul
```

**Function:** RGB with premultiplied alpha.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### UnPremul

```cangjie
UnPremul
```

**Function:** RGB without premultiplied alpha.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Unknown

```cangjie
Unknown
```

**Function:** Unknown transparency.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### func !=(AlphaType)

```cangjie
public operator func !=(other: AlphaType): Bool
```

**Function:** Determines whether two enum values are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AlphaType](#enum-alphatype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are not equal, otherwise returns false. |

### func ==(AlphaType)

```cangjie
public operator func ==(other: AlphaType): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AlphaType](#enum-alphatype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enum. |
```## enum ComponentType

```cangjie
public enum ComponentType <: Equatable<ComponentType> & ToString {
    | YuvY
    | YuvU
    | YuvV
    | Jpeg
    | ...
}
```

**Description:** The component type of an image.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

**Parent Types:**

- Equatable\<ComponentType>
- ToString

### Jpeg

```cangjie
Jpeg
```

**Description:** JPEG type.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

### YuvU

```cangjie
YuvU
```

**Description:** Chrominance information.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

### YuvV

```cangjie
YuvV
```

**Description:** Chrominance information.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

### YuvY

```cangjie
YuvY
```

**Description:** Luminance information.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

### func !=(ComponentType)

```cangjie
public operator func !=(other: ComponentType): Bool
```

**Description:** Determines whether two enumeration values are unequal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ComponentType](#enum-componenttype) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are unequal, otherwise returns false. |

### func ==(ComponentType)

```cangjie
public operator func ==(other: ComponentType): Bool
```

**Description:** Determines whether two enumeration values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ComponentType](#enum-componenttype) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enumeration.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |

## enum DecodingDynamicRange

```cangjie
public enum DecodingDynamicRange <: Equatable<DecodingDynamicRange> & ToString {
    | Auto
    | Sdr
    | Hdr
    | ...
}
```

**Description:** Describes the expected dynamic range of an image during decoding.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parent Types:**

- Equatable\<DecodingDynamicRange>
- ToString

### Auto

```cangjie
Auto
```

**Description:** Adaptive processing based on image information. If the image itself is HDR, it will be decoded as HDR content; otherwise, it will be decoded as SDR content.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Hdr

```cangjie
Hdr
```

**Description:** Processes the image as high dynamic range content.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Sdr

```cangjie
Sdr
```

**Description:** Processes the image as standard dynamic range content.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### func !=(DecodingDynamicRange)

```cangjie
public operator func !=(other: DecodingDynamicRange): Bool
```

**Description:** Determines whether two enumeration values are unequal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [DecodingDynamicRange](#enum-decodingdynamicrange) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are unequal, otherwise returns false. |

### func ==(DecodingDynamicRange)

```cangjie
public operator func ==(other: DecodingDynamicRange): Bool
```

**Description:** Determines whether two enumeration values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [DecodingDynamicRange](#enum-decodingdynamicrange) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enumeration.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |

## enum ImageFormat

```cangjie
public enum ImageFormat <: Equatable<ImageFormat> & ToString {
    | Ycbcr422Sp
    | Jpeg
    | ...
}
```

**Description:** Image format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parent Types:**

- Equatable\<ImageFormat>
- ToString

### Jpeg

```cangjie
Jpeg
```

**Description:** JPEG encoding format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Ycbcr422Sp

```cangjie
Ycbcr422Sp
```

**Description:** YCBCR422 semi-planar format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### func !=(ImageFormat)

```cangjie
public operator func !=(other: ImageFormat): Bool
```

**Description:** Determines whether two enumeration values are unequal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ImageFormat](#enum-imageformat) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are unequal, otherwise returns false. |

### func ==(ImageFormat)

```cangjie
public operator func ==(other: ImageFormat): Bool
```

**Description:** Determines whether two enumeration values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ImageFormat](#enum-imageformat) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enumeration.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |

## enum PackingDynamicRange

```cangjie
public enum PackingDynamicRange <: Equatable<PackingDynamicRange> & ToString {
    | Auto
    | Sdr
    | ...
}
```

**Description:** Describes the expected dynamic range of an image during encoding.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parent Types:**

- Equatable\<PackingDynamicRange>
- ToString

### Auto

```cangjie
Auto
```

**Description:** Adaptive processing based on [pixelmap](#class-pixelmap) content. If the pixelmap itself is HDR, it will be encoded as HDR content; otherwise, it will be encoded as SDR content.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Sdr

```cangjie
Sdr
```

**Description:** Processes the image as standard dynamic range content.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### func !=(PackingDynamicRange)

```cangjie
public operator func !=(other: PackingDynamicRange): Bool
```

**Description:** Determines whether two enumeration values are unequal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [PackingDynamicRange](#enum-packingdynamicrange) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are unequal, otherwise returns false. |

### func ==(PackingDynamicRange)

```cangjie
public operator func ==(other: PackingDynamicRange): Bool
```

**Description:** Determines whether two enumeration values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [PackingDynamicRange](#enum-packingdynamicrange) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enumeration.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |## enum PixelMapFormat

```cangjie
public enum PixelMapFormat <: Equatable<PixelMapFormat> & ToString {
    | Unknown
    | Rgb565
    | Rgba8888
    | Bgra8888
    | Rgb888
    | Alpha8
    | RgbaF16
    | Nv21
    | Nv12
    | Rgba1010102
    | YcbcrP010
    | YcrcbP010
    | ...
}
```

**Description:** Pixel format of images.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parent Types:**

- Equatable\<PixelMapFormat>
- ToString

### Alpha8

```cangjie
Alpha8
```

**Description:** ALPHA_8 format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Bgra8888

```cangjie
Bgra8888
```

**Description:** BGRA_8888 format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Nv12

```cangjie
Nv12
```

**Description:** NV12 format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Nv21

```cangjie
Nv21
```

**Description:** NV21 format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Rgb565

```cangjie
Rgb565
```

**Description:** RGB_565 format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Rgb888

```cangjie
Rgb888
```

**Description:** RGB_888 format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Rgba1010102

```cangjie
Rgba1010102
```

**Description:** RGBA_1010102 format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Rgba8888

```cangjie
Rgba8888
```

**Description:** RGBA_8888 format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### RgbaF16

```cangjie
RgbaF16
```

**Description:** RGBA_F16 format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Unknown

```cangjie
Unknown
```

**Description:** Unknown format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### YcbcrP010

```cangjie
YcbcrP010
```

**Description:** YCBCR_P010 format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### YcrcbP010

```cangjie
YcrcbP010
```

**Description:** YCRCB_P010 format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### func !=(PixelMapFormat)

```cangjie
public operator func !=(other: PixelMapFormat): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[PixelMapFormat](#enum-pixelmapformat)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(PixelMapFormat)

```cangjie
public operator func ==(other: PixelMapFormat): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[PixelMapFormat](#enum-pixelmapformat)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Return Value:**

|Type|Description|
|:----|:----|
|String|Description of the enum.|

## enum PropertyKey

```cangjie
public enum PropertyKey <: ToString & Equatable<PropertyKey> {
    | ImageWidth
    | ImageLength
    | BitsPerSample
    | ImageDescription
    | Make
    | Model
    | Orientation
    | DateTime
    | PhotoMode
    | ExposureTime
    | FNumber
    | GpsLatitudeRef
    | GpsLatitude
    | GpsLongitudeRef
    | GpsLongitude
    | GpsTimeStamp
    | GpsDateStamp
    | IsoSpeedRatings
    | SensitivityType
    | StandardOutputSensitivity
    | RecommendedExposureIndex
    | IsoSpeed
    | DateTimeOriginal
    | ApertureValue
    | ExposureBiasValue
    | MeteringMode
    | LightSource
    | Flash
    | FocalLength
    | SceneFoodConf
    | SceneStageConf
    | SceneBlueSkyConf
    | SceneGreenPlantConf
    | SceneBeachConf
    | SceneSnowConf
    | SceneSunsetConf
    | SceneFlowersConf
    | SceneNightConf
    | SceneTextConf
    | FaceCount
    | CaptureMode
    | RollAngle
    | PitchAngle
    | PhysicalAperture
    | FocusMode
    | UserComment
    | PixelXDimension
    | PixelYDimension
    | SceneType
    | WhiteBalance
    | FocalLengthIn35mmFilm
    | ...
}
```

**Description:** Exchangeable image file format (Exif) information.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parent Types:**

- ToString
- Equatable\<PropertyKey>

### ApertureValue

```cangjie
ApertureValue
```

**Description:** Aperture value.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### BitsPerSample

```cangjie
BitsPerSample
```

**Description:** Bits per pixel.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### CaptureMode

```cangjie
CaptureMode
```

**Description:** Capture mode.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### DateTime

```cangjie
DateTime
```

**Description:** Date and time.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### DateTimeOriginal

```cangjie
DateTimeOriginal
```

**Description:** Shooting time, for example, 2022:09:06 15:48:00.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### ExposureBiasValue

```cangjie
ExposureBiasValue
```

**Description:** Exposure bias value.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### ExposureTime

```cangjie
ExposureTime
```

**Description:** Exposure time, for example, 1/33 sec.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### FNumber

```cangjie
FNumber
```

**Description:** Aperture value, for example, f/1.8.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### FaceCount

```cangjie
FaceCount
```

**Description:** Number of faces.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22### Flash

```cangjie
Flash
```

**Function:** Flash, records flash status.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### FocalLength

```cangjie
FocalLength
```

**Function:** Focal length.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### FocalLengthIn35mmFilm

```cangjie
FocalLengthIn35mmFilm
```

**Function:** Focal length in 35mm film equivalent.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### FocusMode

```cangjie
FocusMode
```

**Function:** Focus mode.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### GpsDateStamp

```cangjie
GpsDateStamp
```

**Function:** GPS date stamp.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### GpsLatitude

```cangjie
GpsLatitude
```

**Function:** Image latitude. When modifying, it should be passed in "degrees, minutes, seconds" format, e.g., "39,54,7.542".

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### GpsLatitudeRef

```cangjie
GpsLatitudeRef
```

**Function:** Latitude reference, e.g., N or S.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### GpsLongitude

```cangjie
GpsLongitude
```

**Function:** Image longitude. When modifying, it should be passed in "degrees, minutes, seconds" format, e.g., "116,19,42.16".

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### GpsLongitudeRef

```cangjie
GpsLongitudeRef
```

**Function:** Longitude reference, e.g., W or E.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### GpsTimeStamp

```cangjie
GpsTimeStamp
```

**Function:** GPS timestamp.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### IsoSpeed

```cangjie
IsoSpeed
```

**Function:** ISO speed rating.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### IsoSpeedRatings

```cangjie
IsoSpeedRatings
```

**Function:** ISO sensitivity, e.g., 400.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### ImageDescription

```cangjie
ImageDescription
```

**Function:** Image information description.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### ImageLength

```cangjie
ImageLength
```

**Function:** Image length.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### ImageWidth

```cangjie
ImageWidth
```

**Function:** Image width.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### LightSource

```cangjie
LightSource
```

**Function:** Light source.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Make

```cangjie
Make
```

**Function:** Manufacturer.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### MeteringMode

```cangjie
MeteringMode
```

**Function:** Metering mode.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Model

```cangjie
Model
```

**Function:** Device model.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### Orientation

```cangjie
Orientation
```

**Function:** Image orientation.<br/>- 1: Top-left, image not rotated.<br/>- 2: Top-right, mirrored horizontally.<br/>- 3: Bottom-right, image rotated 180°.<br/>- 4: Bottom-left, mirrored vertically.<br/>- 5: Left-top, mirrored horizontally then rotated 270° clockwise.<br/>- 6: Right-top, rotated 90° clockwise.<br/>- 7: Right-bottom, mirrored horizontally then rotated 90° clockwise.<br/>- 8: Left-bottom, rotated 270° clockwise.<br/>- Undefined values return "Unknown Value".

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### PhotoMode

```cangjie
PhotoMode
```

**Function:** Photo mode.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### PhysicalAperture

```cangjie
PhysicalAperture
```

**Function:** Physical aperture, f-number.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### PitchAngle

```cangjie
PitchAngle
```

**Function:** Pitch angle.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### PixelXDimension

```cangjie
PixelXDimension
```

**Function:** Pixel X dimension.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### PixelYDimension

```cangjie
PixelYDimension
```

**Function:** Pixel Y dimension.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### RecommendedExposureIndex

```cangjie
RecommendedExposureIndex
```

**Function:** Recommended exposure index.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### RollAngle

```cangjie
RollAngle
```

**Function:** Roll angle.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SceneBeachConf

```cangjie
SceneBeachConf
```

**Function:** Photo scene: beach.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SceneBlueSkyConf

```cangjie
SceneBlueSkyConf
```

**Function:** Photo scene: blue sky.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SceneFlowersConf

```cangjie
SceneFlowersConf
```

**Function:** Photo scene: flowers.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SceneFoodConf

```cangjie
SceneFoodConf
```

**Function:** Photo scene: food.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SceneGreenPlantConf

```cangjie
SceneGreenPlantConf
```

**Function:** Photo scene: green plants.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SceneNightConf

```cangjie
SceneNightConf
```

**Function:** Photo scene: night.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SceneSnowConf

```cangjie
SceneSnowConf
```

**Function:** Photo scene: snow.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SceneStageConf

```cangjie
SceneStageConf
```

**Function:** Photo scene: stage.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SceneSunsetConf

```cangjie
SceneSunsetConf
```

**Function:** Photo scene: sunset.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SceneTextConf

```cangjie
SceneTextConf
```

**Function:** Photo scene: text.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SceneType

```cangjie
SceneType
```

**Function:** Shooting scene mode, e.g., portrait, landscape, sports, night, etc.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### SensitivityType

```cangjie
SensitivityType
```

**Function:** Sensitivity type.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### StandardOutputSensitivity

```cangjie
StandardOutputSensitivity
```

**Function:** Standard output sensitivity.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### UserComment

```cangjie
UserComment
```

**Function:** User comment.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### WhiteBalance

```cangjie
WhiteBalance
```

**Function:** White balance.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### func !=(PropertyKey)

```cangjie
public operator func !=(other: PropertyKey): Bool
```

**Function:** Determines whether two enum values are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PropertyKey](#enum-propertykey) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are not equal, otherwise returns false. |

### func ==(PropertyKey)

```cangjie
public operator func ==(other: PropertyKey): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PropertyKey](#enum-propertykey) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the value of the enum.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enum. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The type is not supported yet. | Invalid enum value, the enum value is not supported. | Check if the passed enum value is correct. |## enum ReceiveType

```cangjie
public enum ReceiveType {
    | ImageArrival
    | ...
}
```

**Function:** Callback type registered when receiving images.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

### ImageArrival

```cangjie
ImageArrival
```

**Function:** Event type when receiving images.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 22

## enum ScaleMode

```cangjie
public enum ScaleMode <: Equatable<ScaleMode> & ToString {
    | FitTargetSize
    | CenterCrop
    | ...
}
```

**Function:** Scaling modes for images.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

**Parent Types:**

- Equatable\<ScaleMode>
- ToString

### CenterCrop

```cangjie
CenterCrop
```

**Function:** Scales the image to fill the target area while center-cropping the excess regions.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### FitTargetSize

```cangjie
FitTargetSize
```

**Function:** Scales the image to fit within the target dimensions.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 22

### func !=(ScaleMode)

```cangjie
public operator func !=(other: ScaleMode): Bool
```

**Function:** Determines if two enum values are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ScaleMode](#enum-scalemode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are not equal, otherwise false.|

### func ==(ScaleMode)

```cangjie
public operator func ==(other: ScaleMode): Bool
```

**Function:** Determines if two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ScaleMode](#enum-scalemode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are equal, otherwise false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the enum value.

**Return Value:**

|Type|Description|
|:----|:----|
|String|Description of the enum value.|

## Additional Notes

### SVG Tag Specifications

Supports SVG tags using version (SVG) 1.1. Currently supported tags include:

- a
- circla
- clipPath
- defs
- ellipse
- feBlend
- feColorMatrix
- feComposite
- feDiffuseLighting
- feDisplacementMap
- feDistantLight
- feFlood
- feGaussianBlur
- feImage
- feMorphology
- feOffset
- fePointLight
- feSpecularLighting
- feSpotLight
- feTurbulence
- filter
- g
- image
- line
- linearGradient
- mask
- path
- pattern
- polygon
- polyline
- radialGradient
- rect
- stop
- svg
- text
- textPath
- tspan
- use