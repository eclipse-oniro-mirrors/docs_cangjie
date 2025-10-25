# ohos.multimedia.image (Image Processing)

This module provides image processing capabilities, including creating PixelMap through attributes, reading image pixel data, and reading image data within a specified region.

## Importing the Module

```cangjie
import kit.ImageKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.
- When running example code, first construct the correct image source through [createImageSource](#func-createimagesourcestring-sourceoptions), which supports building image sources from raw arrays, URIs, file descriptors, etc.

For details about the example project and configuration template mentioned above, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## func createImagePacker()

```cangjie
public func createImagePacker(): ImagePacker
```

**Function:** Creates an ImagePacker instance.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
|[ImagePacker](#class-imagepacker)| Returns an ImagePacker instance. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let imagePacker : ImagePacker = createImagePacker()
```

## func createImageReceiver(Size, ImageFormat, Int32)

```cangjie
public func createImageReceiver(size: Size, format: ImageFormat, capacity: Int32): ImageReceiver
```

**Function:** Creates an ImageReceiver instance by specifying width, height, image format, and capacity.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| size | [Size](#class-size) | Yes | - | The default size of the image. |
| format | [ImageFormat](#enum-imageformat) | Yes | - | The image format, which can be one of the [ImageFormat](#enum-imageformat) constants (currently only ImageFormat:JPEG is supported). |
| capacity | Int32 | Yes | - | The maximum number of images that can be accessed simultaneously. |

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageReceiver](#class-imagereceiver)| If the operation is successful, returns an ImageReceiver instance. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let size = Size(8, 8192)
let receiver:ImageReceiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
```

## func createImageSource(String)

```cangjie
public func createImageSource(uri: String): ImageSource
```

**Function:** Creates an image source instance by passing in a URI.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| uri | String | Yes | - | The image path, currently only supports application sandbox paths. <br>Supported formats include: .jpg, .png, .gif, .bmp, .webp, RAW, [SVG](#svg标签说明). |

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)| Returns an ImageSource class instance. |

## func createImageSource(String, SourceOptions)

```cangjie
public func createImageSource(uri: String, options: SourceOptions): ImageSource
```

**Function:** Creates an image source instance by passing in a URI.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| uri | String | Yes | - | The image path, currently only supports application sandbox paths. <br>Supported formats include: .jpg, .png, .gif, .bmp, .webp, RAW, [SVG](#svg标签说明). |
| options | [SourceOptions](#class-sourceoptions) | Yes | - | Image attributes, including image sequence number and default attribute values. |

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)| Returns an ImageSource class instance. |

## func createImageSource(Int32)

```cangjie
public func createImageSource(fd: Int32): ImageSource
```

**Function:** Creates an image source instance by passing in a file descriptor.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | The file descriptor fd. |

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)| Returns an ImageSource class instance. |

## func createImageSource(Int32, SourceOptions)

```cangjie
public func createImageSource(fd: Int32, options: SourceOptions): ImageSource
```

**Function:** Creates an image source instance by passing in a file descriptor.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | The image file descriptor. |
| options | [SourceOptions](#class-sourceoptions) | Yes | - | Image attributes, including image sequence number and default attribute values. |

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)| Returns an ImageSource class instance. |

## func createImageSource(Array\<UInt8>)

```cangjie
public func createImageSource(buf: Array<UInt8>): ImageSource
```

**Function:** Creates an image source instance by passing in a buffer.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<UInt8> | Yes | - | The image buffer array. |

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)| Returns an ImageSource class instance. |

## func createImageSource(Array\<UInt8>, SourceOptions)

```cangjie
public func createImageSource(buf: Array<UInt8>, options: SourceOptions): ImageSource
```

**Function:** Creates an image source instance by passing in a buffer.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<UInt8> | Yes | - | The image buffer array. |
| options | [SourceOptions](#class-sourceoptions) | Yes | - | Image attributes, including image sequence number and default attribute values. |

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)| Returns an ImageSource class instance. |

## func createImageSource(RawFileDescriptor, SourceOptions)

```cangjie
public func createImageSource(rawfile: RawFileDescriptor, options!: SourceOptions = SourceOptions(0)): ImageSource
```

**Function:** Creates an image source instance by passing in the RawFileDescriptor of an image resource file.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| rawfile | [RawFileDescriptor](../LocalizationKit/cj-apis-raw_file_descriptor.md#class-rawfiledescriptor) | Yes | - | The RawFileDescriptor of the image resource file. |
| options | [SourceOptions](#class-sourceoptions) | No | SourceOptions(0) | **Named parameter.** Image attributes, including pixel density, pixel format, and image size. |

**Return Value:**

| Type | Description |
|:----|:----|
|[ImageSource](#class-imagesource)| Returns an ImageSource class instance. |

## func createPixelMap(Array\<UInt8>, InitializationOptions)

```cangjie
public func createPixelMap(colors: Array<UInt8>, options: InitializationOptions): PixelMap
```

**Function:** Creates a PixelMap by specifying attributes. By default, data is processed in BGRA_8888 format, and currently only BGRA_8888 format is supported.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| colors | Array\<UInt8> | Yes | - | The color array in BGRA_8888 format. |
| options | [InitializationOptions](#class-initializationoptions) | Yes | - | Attributes for creating the pixel, including transparency, size, thumbnail value, pixel format, and editability. |

**Return Value:**

| Type | Description |
|:----|:----|
|[PixelMap](#class-pixelmap)| Returns a PixelMap. <br>If the created pixelmap size exceeds the original image size, the original pixelmap size is returned. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3. Parameter verification failed. |

## class Component

```cangjie
public class Component {
    public let componentType: ComponentType
    public let rowStride: Int32
    public let pixelStride: Int32
    public let byteBuffer: Array<UInt8>
}
```

**Function:** Describes the color components of an image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Initial Version:** 21

### let byteBuffer

```cangjie
public let byteBuffer: Array<UInt8>
```

**Function:** The component buffer.

**Type:** Array\<UInt8>

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Initial Version:** 21

### let componentType

```cangjie
public let componentType: ComponentType
```

**Function:** The component type.

**Type:** [ComponentType](#enum-componenttype)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Initial Version:** 21

### let pixelStride

```cangjie
public let pixelStride: Int32
```

**Function:** The pixel stride.

**Type:** Int32

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Initial Version:** 21

### let rowStride

```cangjie
public let rowStride: Int32
```

**Function:** The row stride.

**Type:** Int32

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Initial Version:** 21

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

**Initial Version:** 21

### var desiredColorSpace

```cangjie
public var desiredColorSpace:?ColorSpaceManager
```

**Function:** The target color space.

**Type:** ?[ColorSpaceManager](../ArkGraphics2D/cj-apis-color_manager.md#class-colorspacemanager)

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

### var desiredDynamicRange

```cangjie
public var desiredDynamicRange: DecodingDynamicRange
```

**Function:** The target dynamic range, with SDR as the default value.

If the platform does not support HDR, the setting is invalid, and the content will be decoded as SDR by default.

**Type:** [DecodingDynamicRange](#enum-decodingdynamicrange)

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

### var desiredPixelFormat

```cangjie
public var desiredPixelFormat: PixelMapFormat
```

**Function:** The decoded pixel format.

**Type:** [PixelMapFormat](#enum-pixelmapformat)

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

### var desiredRegion

```cangjie
public var desiredRegion: Region
```

**Function:** The decoding region.

**Type:** [Region](#class-region)

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

### var desiredSize

```cangjie
public var desiredSize: Size
```

**Function:** The desired output size.

**Type:** [Size](#class-size)

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

### var editable

```cangjie
public var editable: Bool
```

**Function:** Whether the image is editable. When set to false, the image cannot be edited further, and operations such as crop will fail.

**Type:** Bool

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

### var fitDensity

```cangjie
public var fitDensity: Int32
```

**Function:** The image pixel density, in ppi.

**Type:** Int32

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

### var index

```cangjie
public var index: UInt32
```

**Function:** The sequence number of the decoded image.

**Type:** UInt32

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

### var rotate

```cangjie
public var rotate: UInt32
```

**Function:** The rotation angle.

**Type:** UInt32

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

### var sampleSize

```cangjie
public var sampleSize: UInt32
```

**Function:** The thumbnail sampling size, currently only 1 is supported.

**Type:** UInt32

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

### init(UInt32, UInt32, Bool, Size, Region, PixelMapFormat, UInt32, Int32, ?ColorSpaceManager, DecodingDynamicRange)

```cangjie
public init(sampleSize!: UInt32 = 1, rotate!: UInt32 = 0, editable!: Bool = false,
    desiredSize!: Size = Size(0, 0), desiredRegion!: Region = Region(Size(0, 0), 0, 0),
    desiredPixelFormat!: PixelMapFormat = Unknown, index!: UInt32 = 0, fitDensity!: Int32 = 0,
    desiredColorSpace!: ?ColorSpaceManager = None, desiredDynamicRange!: DecodingDynamicRange = Sdr)
```

**Function:** Creates a DecodingOptions object.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| sampleSize | UInt32 | No | 1 | **Named parameter.** The thumbnail sampling size, currently only 1 is supported. |
| rotate | UInt32 | No | 0 | **Named parameter.** The rotation angle. |
| editable | Bool | No | false | **Named parameter.** Whether the image is editable. When set to false, the image cannot## class Image

```cangjie
public class Image {}
```

**Function:** Provides basic image operations, including obtaining image information and reading/writing image data.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### prop clipRect

```cangjie
public prop clipRect: Region
```

**Function:** The region of the image to be cropped.

**Type:** [Region](#class-region)

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### prop format

```cangjie
public prop format: Int32
```

**Function:** The image format, refer to [PixelMapFormat](#enum-pixelmapformat).

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### prop size

```cangjie
public prop size: Size
```

**Function:** The size of the image.

**Type:** [Size](#class-size)

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### func getComponent(ComponentType)

```cangjie
public func getComponent(componentType: ComponentType): Component
```

**Function:** Retrieves the component buffer from the image based on the specified component type and returns the result.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| componentType | [ComponentType](#enum-componenttype) | Yes | - | The component type of the image. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Component](#class-component) | Returns the component buffer. |

### func release()

```cangjie
public func release(): Unit
```

**Function:** Releases the current image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

## class ImageInfo

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

**Function:** Represents image information.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var alphaType

```cangjie
public var alphaType: AlphaType
```

**Function:** Transparency.

**Type:** [AlphaType](#enum-alphatype)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var density

```cangjie
public var density: Int32
```

**Function:** Pixel density, in ppi.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var isHdr

```cangjie
public var isHdr: Bool
```

**Function:** Indicates whether the image is High Dynamic Range (HDR). For [ImageSource](#class-imagesource), it indicates whether the source image is HDR; for [PixelMap](#class-pixelmap), it indicates whether the decoded pixelmap is HDR.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var mimeType

```cangjie
public var mimeType: String
```

**Function:** The actual format of the image (MIME type).

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var pixelFormat

```cangjie
public var pixelFormat: PixelMapFormat
```

**Function:** Pixel format.

**Type:** [PixelMapFormat](#enum-pixelmapformat)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var size

```cangjie
public var size: Size
```

**Function:** The size of the image.

**Type:** [Size](#class-size)

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var stride

```cangjie
public var stride: Int32
```

**Function:** Stride, the space occupied by each row of pixels in memory. stride >= region.size.width*4.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

## class ImagePacker

```cangjie
public class ImagePacker {}
```

**Function:** The image packer class, used for image compression and packaging. Before calling methods of ImagePacker, an ImagePacker instance must be created via [createImagePacker](#func-createimagepacker). Currently supported formats include: jpeg, webp, png.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

### prop supportedFormats

```cangjie
public prop supportedFormats: Array<String>
```

**Function:** The supported formats for image packing: jpeg, webp, png.

**Type:** Array\<String>

**Access:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

### func packToData(ImageSource, PackingOption)

```cangjie
public func packToData(source: ImageSource, options: PackingOption): Array<UInt8>
```

**Function:** Compresses or re-encodes an image.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| source | [ImageSource](#class-imagesource) | Yes | - | The image source to be packed. |
| options | [PackingOption](#class-packingoption) | Yes | - | Sets the packing parameters. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt8> | Used to obtain the compressed or packed data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | If the parameter is invalid. |
  | 62980096 | The operation failed. Possible cause: 1.Image upload exception.2. Decoding process exception. 3. Insufficient memory. |
  | 62980101 | The image data is abnormal. |
  | 62980106 | The image data is too large. This status code is thrown when an error occurs during the process of checking size. |
  | 62980113 | Unknown image format.The image data provided is not in a recognized or supported format, or it may be occorrupted. |
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

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSource: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source, refer to the usage instructions in this document.
var imagePacker = createImagePacker()
let supportedFormats = imagePacker.supportedFormats
let packingOption = PackingOption("image/jpeg", 98)
let packRes = imagePacker.packToData(imageSource, packingOption)
```

### func packToData(PixelMap, PackingOption)

```cangjie
public func packToData(source: PixelMap, options: PackingOption): Array<UInt8>
```

**Function:** Compresses or re-encodes an image.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| source | [PixelMap](#class-pixelmap) | Yes | - | The image source to be packed. |
| options | [PackingOption](#class-packingoption) | Yes | - | Sets the packing parameters. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt8> | Used to obtain the compressed or packed data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | If the parameter is invalid. |
  | 62980096 | The operation failed. Possible cause: 1.Image upload exception.2. Decoding process exception. 3. Insufficient memory. |
  | 62980101 | The image data is abnormal. |
  | 62980106 | The image data is too large. This status code is thrown when an error occurs during the process of checking size. |
  | 62980113 | Unknown image format.The image data provided is not in a recognized or supported format, or it may be occorrupted. |
  | 62980119 | Failed to encode the image. |
  | 62980120 | Add pixelmap out of range. |
  | 62980172 | Failed to encode icc. |
  | 62980252 | Failed to create surface. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

var colors: Array<UInt8> = [80, 2, 4, 8, 40, 2, 4, 8]
var pm = createPixelMap(colors,
    InitializationOptions(Size(2, 1), scaleMode: ScaleMode.CenterCrop))
var imagePacker = createImagePacker()
let supportedFormats = imagePacker.supportedFormats
let packingOption = PackingOption("image/jpeg", 98)
let packRes = imagePacker.packToData(pm, packingOption)
```

### func packToFile(ImageSource, Int32, PackingOption)

```cangjie
public func packToFile(source: ImageSource, fd: Int32, options: PackingOption): Unit
```

**Function:** Encodes the Picture directly into a file with specified encoding parameters.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| source | [ImageSource](#class-imagesource) | Yes | - | The Picture resource to be encoded. |
| fd | Int32 | Yes | - | File descriptor. |
| options | [PackingOption](#class-packingoption) | Yes | - | Sets the packing parameters. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980096 | The operation failed. Possible cause: 1.Image upload exception.2. Decoding process exception. 3. Insufficient memory. |
  | 62980101 | The image data is abnormal. |
  | 62980106 | The image data is too large. This status code is thrown when an error occurs during the process of checking size. |
  | 62980113 | Unknown image format.The image data provided is not in a recognized or supported format, or it may be occorrupted. |
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

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSource: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source, refer to the usage instructions in this document.
var fd: Int32 = 0
let filePath = "data/storage/el1/base/xxx.txt"
let file = FileIo.open(filePath,mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
let packingOption = PackingOption("image/jpeg", 98)
let imagePacker = createImagePacker()
imagePacker.packToFile(imageSource, fd, packingOption)
```

### func packToFile(PixelMap, Int32, PackingOption)

```cangjie
public func packToFile(source: PixelMap, fd: Int32, options: PackingOption): Unit
```

**Function:** Encodes the Picture directly into a file with specified encoding parameters.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| source | [PixelMap](#class-pixelmap) | Yes | - | The Picture resource to be encoded. |
| fd | Int32 | Yes | - | File descriptor. |
| options | [PackingOption](#class-packingoption) | Yes | - | Sets the packing parameters. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980096 | The operation failed. Possible cause: 1.Image upload exception.2. Decoding process exception. 3. Insufficient memory. |
  | 62980101 | The image data is abnormal. |
  | 62980106 | The image data is too large. This status code is thrown when an error occurs during the process of checking size. |
  | 62980113 | Unknown image format.The image data provided is not in a recognized or supported format, or it may be occorrupted. |
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

let color: Array<UInt8> = Array<UInt8>(96, repeat: 0) //96 is the size of the pixel buffer to be created, calculated as: height * width *4
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
```

### func release()

```cangjie
public func release(): Unit
```

**Function:** Releases the image packer instance.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let imagePacker = createImagePacker()
imagePacker.release()
```

## class ImagePropertyOptions

```cangjie
public class ImagePropertyOptions {
    public var index: UInt32
    public var defaultValue: String
    public init(index!: UInt32 = 0, defaultValue!: String = "")
}
```

**Function:** Represents the index for querying image properties.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

### var defaultValue

```cangjie
public var defaultValue: String
```

**Function:** Default property value.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

### var index

```cangjie
public var index: UInt32
```

**Function:** Image sequence number.

**Type:** UInt32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

### init(UInt32, String)

```cangjie
public init(index!: UInt32 = 0, defaultValue!: String = "")
```
**Function:** Creates an ImagePropertyOptions object.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| index | UInt32 | No | 0 | **Named parameter.** Image sequence number. |
| defaultValue | String | No | "" | **Named parameter.** Default property value. |

## class ImageReceiver

```cangjie
public class ImageReceiver {}
```

**Function:** Image receiver class, used to obtain component surface ID, receive the latest image, read the next image, and release the ImageReceiver instance.

An ImageReceiver instance must be created before calling the following methods.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

### prop capacity

```cangjie
public prop capacity: Int32
```

**Function:** Number of images that can be accessed simultaneously.

**Type:** Int32

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

### prop format

```cangjie
public prop format: ImageFormat
```

**Function:** Image format.

**Type:** [ImageFormat](#enum-imageformat)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

### prop size

```cangjie
public prop size: Size
```

**Function:** Image size.

**Type:** [Size](#class-size)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

### func getReceivingSurfaceId()

```cangjie
public func getReceivingSurfaceId(): String
```

**Function:** Used to obtain a surface ID for Camera or other components.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the surface ID. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let size = Size(8, 8192)
var receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
let id: String = receiver.getReceivingSurfaceId()
```

### func release()

```cangjie
public func release(): Unit
```

**Function:** Releases the current image receiver class.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let size = Size(8, 8192)
var receiver = createImageReceiver(size, ImageFormat.Jpeg, 8)
receiver.release()
```

## class ImageSource

```cangjie
public class ImageSource {}
```

**Function:** Image source class, used to obtain image-related information. Before calling ImageSource methods, an ImageSource instance must be created via createImageSource.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

### prop supportedFormats

```cangjie
public prop supportedFormats: Array<String>
```

**Function:** Supported image formats, including: png, jpeg, bmp, gif, webp, RAW.

**Type:** Array\<String>

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

### func createPixelMap(DecodingOptions)

```cangjie
public func createPixelMap(options!: DecodingOptions = DecodingOptions()): PixelMap
```

**Function:** Creates a PixelMap object through image decoding parameters.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

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
```

### func createPixelMapList(DecodingOptions)

```cangjie
public func createPixelMapList(options!: DecodingOptions = DecodingOptions()): Array<PixelMap>
```

**Function:** Creates an array of PixelMap objects through image decoding parameters.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

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
  | 62980096 | The operation failed. Possible causes: 1.Image upload exception. 2.Decoding process exception. 3.Insufficient memory. |
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

### func getDelayTimeList()

```cangjie
public func getDelayTimeList(): Array<Int32>
```

**Function:** Obtains an array of image delay times. This interface is only applicable to GIF images.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Int32> | Returns an array of delay times. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980096 | The operation failed. Possible causes: 1.Image upload exception. 2.Decoding process exception. 3.Insufficient memory. |
  | 62980110 | The image source data is incorrect. |
  | 62980111 | The image source data is incomplete. |
  | 62980115 | Invalid image parameter. |
  | 62980116 | Failed to decode the image. |
  | 62980118 | Failed to create the image plugin. |
  | 62980122 | Failed to decode the image header. |
  | 62980149 | Invalid MIME type for the image source. |

### func getFrameCount()

```cangjie
public func getFrameCount(): UInt32
```

**Function:** Obtains the number of image frames.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Returns the number of image frames. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980096 | The operation failed. Possible causes: 1.Image upload exception. 2.Decoding process exception. 3.Insufficient memory. |
  | 62980111 | The image source data is incomplete. |
  | 62980112 | The image format does not match. |
  | 62980113 | Unknown image format. The image data provided is not in a recognized or supported format, or it may be corrupted. |
  | 62980115 | Invalid image parameter. |
  | 62980116 | Failed to decode the image. |
  | 62980118 | Failed to create the image plugin. |
  | 62980122 | Failed to decode the image header. |
  | 62980137 | Invalid media operation. |

### func getImageInfo(UInt32)

```cangjie
public func getImageInfo(index!: UInt32 = 0): ImageInfo
```

**Function:** Obtains image information.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| index | UInt32 | No | 0 | **Named parameter.** Sequence number when creating the image source. Defaults to 0 if not specified. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ImageInfo](#class-imageinfo) | Returns the obtained image information. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source as per usage instructions.
imageSourceApi.getImageInfo(index : 0)
```

### func getImageProperty(PropertyKey, ImagePropertyOptions)

```cangjie
public func getImageProperty(key: PropertyKey, options!: ImagePropertyOptions = ImagePropertyOptions()): String
```

**Function:** Obtains the value of the specified property key for the image at the given index. Only supports JPEG files with EXIF information.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [PropertyKey](#enum-propertykey) | Yes | - | Image property name. |
| options | [ImagePropertyOptions](#class-imagepropertyoptions) | No | ImagePropertyOptions() | **Named parameter.** Image properties, including image sequence number and default property value. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the image property value. Returns the default property value if failed to obtain. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified; 2.Incorrect parameter types; 3.Parameter verification failed; |
  | 62980096 | The operation failed. Possible causes: 1.Image upload exception. 2.Decoding process exception. 3.Insufficient memory. |
  | 62980103 | The image data is not supported. |
  | 62980110 | The image source data is incorrect. |
  | 62980111 | The image source data is incomplete. |
  | 62980112 | The image format does not match. |
  | 62980113 | Unknown image format. The image data provided is not in a recognized or supported format, or it may be corrupted. |
  | 62980115 | Invalid image parameter. |
  | 62980118 | Failed to create the image plugin. |
  | 62980122 | Failed to decode the image header. |
  | 62980123 | The image does not support EXIF decoding. |
  | 62980135 | The EXIF value is invalid. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source as per usage instructions.
imageSourceApi.getImageProperty(PropertyKey.ImageLength)
```

### func modifyImageProperty(PropertyKey, String)

```cangjie
public func modifyImageProperty(key: PropertyKey, value: String): Unit
```

**Function:** Modifies the value of an image property through the specified key. Only supports JPEG files with EXIF information.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | [PropertyKey](#enum-propertykey) | Yes | - | Image property name. |
| value | String | Yes | - | Property value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified; 2.Incorrect parameter types; |
  | 62980123 | The image does not support EXIF decoding. |
  | 62980133 | The EXIF data is out of range. |
  | 62980135 | The EXIF value is invalid. |
  | 62980146 | The EXIF data failed to be written to the file. |

### func release()

```cangjie
public func release(): Unit
```

**Function:** Releases the image source instance.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source as per usage instructions.
imageSourceApi.release()
```

### func updateData(Array\<UInt8>, Bool, UInt32, UInt32)

```cangjie
public func updateData(buf: Array<UInt8>, isFinished: Bool, offset: UInt32, length: UInt32): Unit
```

**Function:** Updates incremental data, used in conjunction with CreateIncrementalSource.

**System Capability:** SystemCapability.Multimedia.Image.ImageSource

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<UInt8> | Yes | - | Incremental data. |
| isFinished | Bool | Yes | - | Whether the update is complete. |
| offset | UInt32 | Yes | - | Offset. |
| length | UInt32 | Yes | - | Array length. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source as per usage instructions.
let testPng = Array<UInt8>(16500, repeat: 0)
let bufferSize = 5000
var offset = 0
var isFinished = false
while (offset < testPng.size) {
    var oneStep = testPng.slice(offset, min(bufferSize, testPng.size - offset))
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

**Since:** 21

### var alphaType

```cangjie
public var alphaType: AlphaType
```

**Function:** Transparency.

**Type:** [AlphaType](#enum-alphatype)

**Access:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var editable

```cangjie
public var editable: Bool
```

**Function:** Whether it is editable.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var pixelFormat

```cangjie
public var pixelFormat: PixelMapFormat
```

**Function:** Pixel format.

**Type:** [PixelMapFormat](#enum-pixelmapformat)

**Access:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var scaleMode

```cangjie
public var scaleMode: ScaleMode
```

**Function:** Scaling mode.

**Type:** [ScaleMode](#enum-scalemode)

**Access:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var size

```cangjie
public var size: Size
```

**Function:** Size of the created image.

**Type:** [Size](#class-size)

**Access:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var srcPixelFormat

```cangjie
public var srcPixelFormat: PixelMapFormat
```

**Function:** Pixel format of the input buffer data. Default value is BGRA_8888.

**Type:** [PixelMapFormat](#enum-pixelmapformat)

**Access:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### init(Size, AlphaType, Bool, PixelMapFormat, PixelMapFormat, ScaleMode)

```cangjie
public init(size: Size, alphaType!: AlphaType = AlphaType.Premul, editable!: Bool = false, srcPixelFormat!: PixelMapFormat = PixelMapFormat.Bgra8888,
    pixelFormat!: PixelMapFormat = PixelMapFormat.Bgra8888, scaleMode!: ScaleMode = ScaleMode.FitTargetSize)
```

**Function:** Creates an InitializationOptions object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Size](#class-size) | Yes | - | **Named parameter.** Size of the created image. |
| alphaType | [AlphaType](#enum-alphatype) | No | AlphaType.Premul | **Named parameter.** Transparency. |
| editable | Bool | No | false | **Named parameter.** Whether it is editable. |
| srcPixelFormat | [PixelMapFormat](#enum-pixelmapformat) | No | PixelMapFormat.Bgra8888 | **Named parameter.** Pixel format of the input buffer data. |
| pixelFormat | [PixelMapFormat](#enum-pixelmapformat) | No | PixelMapFormat.Bgra8888 | **Named parameter.** Pixel format. |
| scaleMode | [ScaleMode](#enum-scalemode) | No | ScaleMode.FitTargetSize | **Named parameter.** Scaling mode. |

## class PackingOption

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

**Since:** 21

### var bufferSize

```cangjie
public var bufferSize: UInt64
```

**Function:** Size of the buffer for receiving encoded data, in bytes. If not set, defaults to 25MB. If the encoded image exceeds 25MB, this parameter must be specified. bufferSize must be larger than the size of the encoded image. This parameter does not apply to [packToFile](#func-packtofileimagesource-int32-packingoption).

**Type:** UInt64

**Access:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

### var desiredDynamicRange

```cangjie
public var desiredDynamicRange: PackingDynamicRange
```

**Function:** Target dynamic range. Default is SDR.

**Type:** [PackingDynamicRange](#enum-packingdynamicrange)

**Access:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

### var format

```cangjie
public var format: String
```

**Function:** Target format.</br>Currently supports "image/jpeg", "image/webp", "image/png", and "image/heif" (availability varies by hardware device).

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

### var needsPackProperties

```cangjie
public var needsPackProperties: Bool
```

**Function:** Whether to encode image property information, such as EXIF. Default is false.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

### var quality

```cangjie
public var quality: UInt8
```

**Function:** Parameter for setting output image quality in JPEG encoding, ranging from 0-100. 0 is the lowest quality, 100 is the highest. Higher quality results in larger file sizes.

**Type:** UInt8

**Access:** Read-Write

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

### init(String, UInt8, UInt64, PackingDynamicRange, Bool)

```cangjie
public init(format: String, quality: UInt8, bufferSize!: UInt64 = 0,
    desiredDynamicRange!: PackingDynamicRange = Sdr, needsPackProperties!: Bool = false)
```

**Function:** Creates a PackingOption object.

**System Capability:** SystemCapability.Multimedia.Image.ImagePacker

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| format | String | Yes | - | Target format.</br>Currently supports "image/jpeg", "image/webp", "image/png", and "image/heif" (availability varies by hardware device). |
| quality | UInt8 | Yes | - | Parameter for setting output image quality in JPEG encoding, ranging from 0-100. 0 is the lowest quality, 100 is the highest. Higher quality results in larger file sizes. |
| bufferSize | UInt64 | No | 0 | **Named parameter.** Size of the buffer for receiving encoded data, in bytes. If not set, defaults to 25MB. If the encoded image exceeds 25MB, this parameter must be specified. bufferSize must be larger than the size of the encoded image. This parameter does not apply to [packToFile](#func-packtofileimagesource-int32-packingoption). |
| desiredDynamicRange | [PackingDynamicRange](#enum-packingdynamicrange) | No | Sdr | **Named parameter.** Target dynamic range. |
| needsPackProperties | Bool | No | false | **Named parameter.** Whether to encode image property information, such as EXIF. |

## class PixelMap

```cangjie
public class PixelMap {}
```

**Function:** Image pixel class for reading or writing image data and obtaining image information. Before calling PixelMap methods, a PixelMap instance must be created via [createPixelMap](#func-createpixelmaparrayuint8-initializationoptions). Currently, the maximum serialized size of pixelmap is 128MB; exceeding this will cause display failure. Size is calculated as (width * height * bytes per pixel).

PixelMap supports cross-thread calls via Worker. After PixelMap is transferred across threads via Worker, all interfaces of the original thread's PixelMap cannot be called; otherwise, error 501 (server does not support the functionality required to fulfill the request) will occur.

Before calling PixelMap methods, a PixelMap object must be created via [createPixelMap](#func-createpixelmaparrayuint8-initializationoptions).

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### prop isEditable

```cangjie
public prop isEditable: Bool
```

**Function:** Sets whether the image pixels can be edited.

**Type:** Bool

**Access:** Read-Only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### prop isStrideAlignment

```cangjie
public prop isStrideAlignment: Bool
```

**Function:** Sets whether the image memory is DMA memory.

**Type:** Bool

**Access:** Read-Only

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### func applyColorSpace(ColorSpaceManager)

```cangjie
public func applyColorSpace(targetColorSpace: ColorSpaceManager): Unit
```

**Function:** Performs color space conversion on image pixels based on the input target color space.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| targetColorSpace | [ColorSpaceManager](../ArkGraphics2D/cj-apis-color_manager.md#class-colorspacemanager) | Yes | - | Target color space, supports Srgb, DCI_P3, DisplayP3, ADOBE_RGB_1998. |

**Exceptions:**

- BusinessException: Error codes as shown below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | The parameter check failed. |
  | 62980104 | Failed to initialize the internal object. |
  | 62980108 | Failed to convert the color space. |
  | 62980115 | Invalid image parameter. |

### func createAlphaPixelmap()

```cangjie
public func createAlphaPixelmap(): PixelMap
```

**Function:** Generates a pixelmap containing only alpha channel information based on the alpha channel, which can be used for shadow effects.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

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

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source as per usage instructions.
let pixelMap = imageSourceApi.createPixelMap()
let alphaPixelmap = pixelMap.createAlphaPixelmap()
```

### func crop(Region)

```cangjie
public func crop(region: Region): Unit
```

**Function:** Crops the image based on the input dimensions.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

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

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source as per usage instructions.
let pixelMap = imageSourceApi.createPixelMap()
let region: Region = Region(Size(100, 100), 0, 0)
pixelMap.crop(region)
```### func flip(Bool, Bool)

```cangjie
public func flip(horizontal: Bool, vertical: Bool): Unit
```

**Function:** Flips the image based on input conditions.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| horizontal | Bool | Yes | - | Horizontal flip. |
| vertical | Bool | Yes | - | Vertical flip. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
let pixelMap = imageSourceApi.createPixelMap()
let horizontal: Bool = true
let vertical: Bool = false
pixelMap.flip(horizontal, vertical)
```

### func getBytesNumberPerRow()

```cangjie
public func getBytesNumberPerRow(): UInt32
```

**Function:** Gets the number of bytes per row of the image pixels.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | The number of bytes per row of the image pixels. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
let pixelMap = imageSourceApi.createPixelMap()
let rowCount : UInt32 = pixelMap.getBytesNumberPerRow()
```

### func getColorSpace()

```cangjie
public func getColorSpace(): ColorSpaceManager
```

**Function:** Gets the wide color gamut information of the image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [ColorSpaceManager](../ArkGraphics2D/cj-apis-color_manager.md#class-colorspacemanager) | The wide color gamut information of the image. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980101 | If the image data is abnormal. |
  | 62980103 | If the image data is unsupported. |
  | 62980115 | If the image parameter is invalid. |

### func getDensity()

```cangjie
public func getDensity(): Int32
```

**Function:** Gets the density of the current image pixels.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | The density of the image pixels. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
let pixelMap = imageSourceApi.createPixelMap()
let getDensity : Int32 = pixelMap.getDensity()
```

### func getImageInfo()

```cangjie
public func getImageInfo(): ImageInfo
```

**Function:** Gets the pixel information of the image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [ImageInfo](#class-imageinfo) | Used to get the pixel information of the image. Returns an error message on failure. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
let pixelMap = imageSourceApi.createPixelMap()
pixelMap.getImageInfo()
```

### func getPixelBytesNumber()

```cangjie
public func getPixelBytesNumber(): UInt32
```

**Function:** Gets the total number of bytes of the image pixels.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | The total number of bytes of the image pixels. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
let pixelMap = imageSourceApi.createPixelMap()
let pixelBytesNumber : UInt32 = pixelMap.getPixelBytesNumber()
```

### func opacity(Float32)

```cangjie
public func opacity(rate: Float32): Unit
```

**Function:** Sets the transparency ratio to achieve the corresponding transparency effect for the PixelMap.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| rate | Float32 | Yes | - | The value of the transparency ratio. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
let pixelMap = imageSourceApi.createPixelMap()
let rate: Float32 = 0.5
pixelMap.opacity(rate)
```

### func readPixels(PositionArea)

```cangjie
public func readPixels(area: PositionArea): Unit
```

**Function:** Reads the image data within the specified area.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| area | [PositionArea](#class-positionarea) | Yes | - | The area size. Reads based on the area. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

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
```

### func readPixelsToBuffer(Array\<UInt8>)

```cangjie
public func readPixelsToBuffer(dst: Array<UInt8>): Unit
```

**Function:** Reads the image pixel data and writes the result into an Array\<UInt8>. If the pixelmap is created with the BGRA_8888 format, the read pixel data will be consistent with the original data.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| dst | Array\<UInt8> | Yes | - | The buffer where the image pixel data will be written after the function executes. The buffer size is obtained via the [getPixelBytesNumber](#func-getpixelbytesnumber) interface. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
let pixelMap = imageSourceApi.createPixelMap()
let readBuffer: Array<UInt8> = Array<UInt8>(96, repeat: 0) //96 is the required pixel buffer size, calculated as: height * width *4
pixelMap.readPixelsToBuffer(readBuffer)
```

### func release()

```cangjie
public func release(): Unit
```

**Function:** Releases the PixelMap object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
let pixelMap = imageSourceApi.createPixelMap()
pixelMap.release()
```

### func rotate(Float32)

```cangjie
public func rotate(angle: Float32): Unit
```

**Function:** Rotates the image based on the input angle.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| angle | Float32 | Yes | - | The rotation angle of the image. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
let pixelMap = imageSourceApi.createPixelMap()
let angle: Float32 = 90.0
pixelMap.rotate(angle)
```

### func scale(Float32, Float32)

```cangjie
public func scale(x: Float32, y: Float32): Unit
```

**Function:** Scales the image based on the input width and height.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| x | Float32 | Yes | - | The scaling factor for width. |
| y | Float32 | Yes | - | The scaling factor for height. |

### func setColorSpace(ColorSpaceManager)

```cangjie
public func setColorSpace(colorSpace: ColorSpaceManager): Unit
```

**Function:** Sets the wide color gamut information of the image.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| colorSpace | [ColorSpaceManager](../ArkGraphics2D/cj-apis-color_manager.md#class-colorspacemanager) | Yes | - | The wide color gamut information of the image. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Image Error Codes](./cj-errorcode-image.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 62980111 | The image source data is incomplete. |
  | 62980115 | If the image parameter is invalid. |

### func translate(Float32, Float32)

```cangjie
public func translate(x: Float32, y: Float32): Unit
```

**Function:** Transforms the position of the image based on the input coordinates.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| x | Float32 | Yes | - | The horizontal coordinate of the area. |
| y | Float32 | Yes | - | The vertical coordinate of the area. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
let pixelMap = imageSourceApi.createPixelMap()
let translateX: Float32 = 50.0
let translateY: Float32 = 10.0
pixelMap.translate(translateX, translateY)
```

### func writeBufferToPixels(Array\<UInt8>)

```cangjie
public func writeBufferToPixels(src: Array<UInt8>): Unit
```

**Function:** Reads the image data from the buffer and writes the result into the PixelMap.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| src | Array\<UInt8> | Yes | - | The image pixel data. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

let data: Array<UInt8> = Array<UInt8>(112, repeat: 0)
let sourceOptions: SourceOptions = SourceOptions(120)
let imageSourceApi: ImageSource = createImageSource(data, sourceOptions)  // Replace with the correct image source. Refer to the usage instructions in this document.
let pixelMap = imageSourceApi.createPixelMap()
let color: Array<UInt8> = Array<UInt8>(96, {i => UInt8(i)}) //96 is the required pixel buffer size, calculated as: height * width *4
pixelMap.writeBufferToPixels(color)
```

### func writePixels(PositionArea)

```cangjie
public func writePixels(area: PositionArea): Unit
```

**Function:** Writes the PixelMap into the specified area.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| area | [PositionArea](#class-positionarea) | Yes | - | The area to write into. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ImageKit.*

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
```## class PositionArea

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

**Since:** 21

### var offset

```cangjie
public var offset: UInt32
```

**Function:** Offset.

**Type:** UInt32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var pixels

```cangjie
public var pixels: Array<UInt8>
```

**Function:** Pixels.

**Type:** Array\<UInt8>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var region

```cangjie
public var region: Region
```

**Function:** Region for read/write operations. The sum of the region width and X-coordinate must not exceed the original image width, and the sum of the region height and Y-coordinate must not exceed the original image height.

**Type:** [Region](#class-region)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var stride

```cangjie
public var stride: UInt32
```

**Function:** Stride, the space occupied by each row of pixels in memory. stride >= region.size.width*4.

**Type:** UInt32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### init(Array\<UInt8>, UInt32, UInt32, Region)

```cangjie
public init(pixels: Array<UInt8>, offset: UInt32, stride: UInt32, region: Region)
```

**Function:** Creates a PositionArea object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| pixels | Array\<UInt8> | Yes | - | Pixels. |
| offset | UInt32 | Yes | - | Offset. |
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

**Since:** 21

### var size

```cangjie
public var size: Size
```

**Function:** Region size.

**Type:** [Size](#class-size)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var x

```cangjie
public var x: Int32
```

**Function:** X-coordinate of the region.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var y

```cangjie
public var y: Int32
```

**Function:** Y-coordinate of the region.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### init(Size, Int32, Int32)

```cangjie
public init(size: Size, x: Int32, y: Int32)
```

**Function:** Creates a Region object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
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

**Since:** 21

### var height

```cangjie
public var height: Int32
```

**Function:** Height of the output image.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var width

```cangjie
public var width: Int32
```

**Function:** Width of the output image.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### init(Int32, Int32)

```cangjie
public init(height: Int32, width: Int32)
```

**Function:** Creates a Size object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
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

**Since:** 21

### var sourceDensity

```cangjie
public var sourceDensity: Int32
```

**Function:** Pixel density of the image resource, in DPI.

When the desiredSize in [DecodingOptions](#class-decodingoptions) is not set, and both SourceOptions.sourceDensity and DecodingOptions.fitDensity are non-zero, the decoded output pixelmap will be scaled.

The scaled width is calculated as follows (same for height): (width * fitDensity + (sourceDensity >> 1)) / sourceDensity.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var sourcePixelFormat

```cangjie
public var sourcePixelFormat: PixelMapFormat
```

**Function:** Pixel format of the image, default is UNKNOWN.

**Type:** [PixelMapFormat](#enum-pixelmapformat)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### var sourceSize

```cangjie
public var sourceSize: Size
```

**Function:** Pixel size of the image, default is empty.

**Type:** [Size](#class-size)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### init(Int32, PixelMapFormat, Size)

```cangjie
public init(sourceDensity: Int32, sourcePixelFormat!: PixelMapFormat = PixelMapFormat.Unknown, sourceSize!: Size = Size(0, 0))
```

**Function:** Creates a SourceOptions object.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| sourceDensity | Int32 | Yes | - | Pixel density of the image resource, in DPI.<br>When the desiredSize in [DecodingOptions](#class-decodingoptions) is not set, and both SourceOptions.sourceDensity and DecodingOptions.fitDensity are non-zero, the decoded output pixelmap will be scaled.<br>The scaled width is calculated as follows (same for height): (width * fitDensity + (sourceDensity >> 1)) / sourceDensity. |
| sourcePixelFormat | [PixelMapFormat](#enum-pixelmapformat) | No | PixelMapFormat.Unknown | **Named parameter** Pixel format of the image, default is UNKNOWN. |
| sourceSize | [Size](#class-size) | No | Size(0, 0) | **Named parameter** Pixel size of the image, default is empty. |

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

**Since:** 21

**Parent Types:**

- Equatable\<AlphaType>
- ToString

### Opaque

```cangjie
Opaque
```

**Function:** No alpha or the image is opaque.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Premul

```cangjie
Premul
```

**Function:** RGB with premultiplied alpha.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### UnPremul

```cangjie
UnPremul
```

**Function:** RGB without premultiplied alpha.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Unknown

```cangjie
Unknown
```

**Function:** Unknown transparency.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### func !=(AlphaType)

```cangjie
public operator func !=(other: AlphaType): Bool
```

**Function:** Determines if two enum values are not equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [AlphaType](#enum-alphatype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are not equal, otherwise false. |

### func ==(AlphaType)

```cangjie
public operator func ==(other: AlphaType): Bool
```

**Function:** Determines if two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [AlphaType](#enum-alphatype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enum. |## enum ComponentType

```cangjie
public enum ComponentType <: Equatable<ComponentType> & ToString {
    | YuvY
    | YuvU
    | YuvV
    | Jpeg
    | ...
}
```

**Function:** Image component type.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

**Parent Types:**

- Equatable\<ComponentType>
- ToString

### Jpeg

```cangjie
Jpeg
```

**Function:** JPEG type.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

### YuvU

```cangjie
YuvU
```

**Function:** Chrominance information.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

### YuvV

```cangjie
YuvV
```

**Function:** Chrominance information.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

### YuvY

```cangjie
YuvY
```

**Function:** Luminance information.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

### func !=(ComponentType)

```cangjie
public operator func !=(other: ComponentType): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ComponentType](#enum-componenttype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

### func ==(ComponentType)

```cangjie
public operator func ==(other: ComponentType): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ComponentType](#enum-componenttype) | Yes | - | Another enum value. |

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

## enum DecodingDynamicRange

```cangjie
public enum DecodingDynamicRange <: Equatable<DecodingDynamicRange> & ToString {
    | Auto
    | Sdr
    | Hdr
    | ...
}
```

**Function:** Describes the expected dynamic range of the image during decoding.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parent Types:**

- Equatable\<DecodingDynamicRange>
- ToString

### Auto

```cangjie
Auto
```

**Function:** Adaptive processing based on image information. If the image itself is HDR, it will be decoded as HDR content; otherwise, it will be decoded as SDR content.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Hdr

```cangjie
Hdr
```

**Function:** Processes the image as high dynamic range.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Sdr

```cangjie
Sdr
```

**Function:** Processes the image as standard dynamic range.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### func !=(DecodingDynamicRange)

```cangjie
public operator func !=(other: DecodingDynamicRange): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [DecodingDynamicRange](#enum-decodingdynamicrange) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

### func ==(DecodingDynamicRange)

```cangjie
public operator func ==(other: DecodingDynamicRange): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [DecodingDynamicRange](#enum-decodingdynamicrange) | Yes | - | Another enum value. |

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

## enum ImageFormat

```cangjie
public enum ImageFormat <: Equatable<ImageFormat> & ToString {
    | Ycbcr422Sp
    | Jpeg
    | ...
}
```

**Function:** Image format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parent Types:**

- Equatable\<ImageFormat>
- ToString

### Jpeg

```cangjie
Jpeg
```

**Function:** JPEG encoding format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Ycbcr422Sp

```cangjie
Ycbcr422Sp
```

**Function:** YCBCR422 semi-planar format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### func !=(ImageFormat)

```cangjie
public operator func !=(other: ImageFormat): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageFormat](#enum-imageformat) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

### func ==(ImageFormat)

```cangjie
public operator func ==(other: ImageFormat): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageFormat](#enum-imageformat) | Yes | - | Another enum value. |

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

## enum PackingDynamicRange

```cangjie
public enum PackingDynamicRange <: Equatable<PackingDynamicRange> & ToString {
    | Auto
    | Sdr
    | ...
}
```

**Function:** Describes the expected dynamic range of the image during encoding.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parent Types:**

- Equatable\<PackingDynamicRange>
- ToString

### Auto

```cangjie
Auto
```

**Function:** Adaptive processing based on [pixelmap](#class-pixelmap) content. If the pixelmap itself is HDR, it will be encoded as HDR content; otherwise, it will be encoded as SDR content.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Sdr

```cangjie
Sdr
```

**Function:** Processes the image as standard dynamic range.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### func !=(PackingDynamicRange)

```cangjie
public operator func !=(other: PackingDynamicRange): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PackingDynamicRange](#enum-packingdynamicrange) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

### func ==(PackingDynamicRange)

```cangjie
public operator func ==(other: PackingDynamicRange): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PackingDynamicRange](#enum-packingdynamicrange) | Yes | - | Another enum value. |

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
| String | Description of the enum. |## enum PixelMapFormat

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

**Since:** 21

**Parent Types:**

- Equatable\<PixelMapFormat>
- ToString

### Alpha8

```cangjie
Alpha8
```

**Description:** Format ALPHA_8.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Bgra8888

```cangjie
Bgra8888
```

**Description:** Format BGRA_8888.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Nv12

```cangjie
Nv12
```

**Description:** Format NV12.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Nv21

```cangjie
Nv21
```

**Description:** Format NV21.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Rgb565

```cangjie
Rgb565
```

**Description:** Format RGB_565.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Rgb888

```cangjie
Rgb888
```

**Description:** Format RGB_888.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Rgba1010102

```cangjie
Rgba1010102
```

**Description:** Format RGBA_1010102.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Rgba8888

```cangjie
Rgba8888
```

**Description:** Format RGBA_8888.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### RgbaF16

```cangjie
RgbaF16
```

**Description:** Format RGBA_F16.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Unknown

```cangjie
Unknown
```

**Description:** Unknown format.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### YcbcrP010

```cangjie
YcbcrP010
```

**Description:** Format YCBCR_P010.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### YcrcbP010

```cangjie
YcrcbP010
```

**Description:** Format YCRCB_P010.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

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

**Description:** EXIF (Exchangeable Image File Format) image information.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parent Types:**

- ToString
- Equatable\<PropertyKey>

### ApertureValue

```cangjie
ApertureValue
```

**Description:** Aperture value.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### BitsPerSample

```cangjie
BitsPerSample
```

**Description:** Bits per pixel.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### CaptureMode

```cangjie
CaptureMode
```

**Description:** Capture mode.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### DateTime

```cangjie
DateTime
```

**Description:** Date and time.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### DateTimeOriginal

```cangjie
DateTimeOriginal
```

**Description:** Shooting time, e.g., 2022:09:06 15:48:00.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### ExposureBiasValue

```cangjie
ExposureBiasValue
```

**Description:** Exposure bias value.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### ExposureTime

```cangjie
ExposureTime
```

**Description:** Exposure time, e.g., 1/33 sec.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### FNumber

```cangjie
FNumber
```

**Description:** Aperture value, e.g., f/1.8.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### FaceCount

```cangjie
FaceCount
```

**Description:** Number of faces.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21### Flash

```cangjie
Flash
```

**Function:** Flashlight, records the flash status.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### FocalLength

```cangjie
FocalLength
```

**Function:** Focal length.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### FocalLengthIn35mmFilm

```cangjie
FocalLengthIn35mmFilm
```

**Function:** Focal length in 35mm film equivalent.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### FocusMode

```cangjie
FocusMode
```

**Function:** Focus mode.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### GpsDateStamp

```cangjie
GpsDateStamp
```

**Function:** GPS date stamp.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### GpsLatitude

```cangjie
GpsLatitude
```

**Function:** Image latitude. When modifying, input should follow "degrees,minutes,seconds" format, e.g., "39,54,7.542".

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### GpsLatitudeRef

```cangjie
GpsLatitudeRef
```

**Function:** Latitude reference, e.g., N or S.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### GpsLongitude

```cangjie
GpsLongitude
```

**Function:** Image longitude. When modifying, input should follow "degrees,minutes,seconds" format, e.g., "116,19,42.16".

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### GpsLongitudeRef

```cangjie
GpsLongitudeRef
```

**Function:** Longitude reference, e.g., W or E.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### GpsTimeStamp

```cangjie
GpsTimeStamp
```

**Function:** GPS timestamp.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### IsoSpeed

```cangjie
IsoSpeed
```

**Function:** ISO speed rating.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### IsoSpeedRatings

```cangjie
IsoSpeedRatings
```

**Function:** ISO sensitivity, e.g., 400.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### ImageDescription

```cangjie
ImageDescription
```

**Function:** Image information description.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### ImageLength

```cangjie
ImageLength
```

**Function:** Image length.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### ImageWidth

```cangjie
ImageWidth
```

**Function:** Image width.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### LightSource

```cangjie
LightSource
```

**Function:** Light source.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Make

```cangjie
Make
```

**Function:** Manufacturer.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### MeteringMode

```cangjie
MeteringMode
```

**Function:** Metering mode.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Model

```cangjie
Model
```

**Function:** Device model.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### Orientation

```cangjie
Orientation
```

**Function:** Image orientation.<br/>- 1: Top-left, image not rotated.<br/>- 2: Top-right, mirrored horizontally.<br/>- 3: Bottom-right, image rotated 180°.<br/>- 4: Bottom-left, mirrored vertically.<br/>- 5: Left-top, mirrored horizontally then rotated 270° clockwise.<br/>- 6: Right-top, rotated 90° clockwise.<br/>- 7: Right-bottom, mirrored horizontally then rotated 90° clockwise.<br/>- 8: Left-bottom, rotated 270° clockwise.<br/>- Undefined values return "Unknown Value".

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### PhotoMode

```cangjie
PhotoMode
```

**Function:** Photo capture mode.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### PhysicalAperture

```cangjie
PhysicalAperture
```

**Function:** Physical aperture, lens opening size.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### PitchAngle

```cangjie
PitchAngle
```

**Function:** Pitch angle.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### PixelXDimension

```cangjie
PixelXDimension
```

**Function:** Pixel X dimension.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### PixelYDimension

```cangjie
PixelYDimension
```

**Function:** Pixel Y dimension.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### RecommendedExposureIndex

```cangjie
RecommendedExposureIndex
```

**Function:** Recommended exposure index.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### RollAngle

```cangjie
RollAngle
```

**Function:** Roll angle.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SceneBeachConf

```cangjie
SceneBeachConf
```

**Function:** Photo scene: beach.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SceneBlueSkyConf

```cangjie
SceneBlueSkyConf
```

**Function:** Photo scene: blue sky.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SceneFlowersConf

```cangjie
SceneFlowersConf
```

**Function:** Photo scene: flowers.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SceneFoodConf

```cangjie
SceneFoodConf
```

**Function:** Photo scene: food.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SceneGreenPlantConf

```cangjie
SceneGreenPlantConf
```

**Function:** Photo scene: green plants.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SceneNightConf

```cangjie
SceneNightConf
```

**Function:** Photo scene: night.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SceneSnowConf

```cangjie
SceneSnowConf
```

**Function:** Photo scene: snow.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SceneStageConf

```cangjie
SceneStageConf
```

**Function:** Photo scene: stage.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SceneSunsetConf

```cangjie
SceneSunsetConf
```

**Function:** Photo scene: sunset.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SceneTextConf

```cangjie
SceneTextConf
```

**Function:** Photo scene: text.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SceneType

```cangjie
SceneType
```

**Function:** Photo scene mode, e.g., portrait, landscape, sports, night, etc.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### SensitivityType

```cangjie
SensitivityType
```

**Function:** Sensitivity type.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### StandardOutputSensitivity

```cangjie
StandardOutputSensitivity
```

**Function:** Standard output sensitivity.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### UserComment

```cangjie
UserComment
```

**Function:** User comment.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### WhiteBalance

```cangjie
WhiteBalance
```

**Function:** White balance.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

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

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enum. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The type is not supported yet. | Invalid enum value, the enum value is not supported. | Check if the input enum value is correct. |## enum ReceiveType

```cangjie
public enum ReceiveType {
    | ImageArrival
    | ...
}
```

**Function:** Callback registration type for receiving images.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

### ImageArrival

```cangjie
ImageArrival
```

**Function:** Event type when receiving images.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

## enum ScaleMode

```cangjie
public enum ScaleMode <: Equatable<ScaleMode> & ToString {
    | FitTargetSize
    | CenterCrop
    | ...
}
```

**Function:** Image scaling modes.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

**Parent Types:**

- Equatable\<ScaleMode>
- ToString

### CenterCrop

```cangjie
CenterCrop
```

**Function:** Scales the image to fill the target area while center-cropping the excess regions.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### FitTargetSize

```cangjie
FitTargetSize
```

**Function:** Scales the image to fit within the target dimensions.

**System Capability:** SystemCapability.Multimedia.Image.Core

**Since:** 21

### func !=(ScaleMode)

```cangjie
public operator func !=(other: ScaleMode): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ScaleMode](#enum-scalemode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are unequal, otherwise false.|

### func ==(ScaleMode)

```cangjie
public operator func ==(other: ScaleMode): Bool
```

**Function:** Determines whether two enum values are equal.

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

**Function:** Gets the value of the enum.

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