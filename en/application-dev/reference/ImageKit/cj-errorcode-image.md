# Image Error Codes

> **Note:**
>
> The following describes only the module-specific error codes. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 501 Unable to Invoke Interface

**Error Message**

Resource unavailable.

**Possible Causes**

The image was passed across threads, making the original object unable to invoke the interface.

**Resolution Steps**

Check the image and re-decode it following the specified instructions.

## 62980096 Operation Failed

**Error Message**

Transaction operation failed.

**Possible Causes**

1. An exception occurred during image upload.
2. Other operations were performed during decoding.
3. Image decoding was not performed as instructed.
4. Insufficient device memory.
5. Decoding library processing failed.

**Resolution Steps**

Check the image and re-decode it following the specified instructions.

## 62980097 Operation Failed

**Error Message**

Rpc error.

**Possible Causes**

1. An exception occurred during image upload.
2. Other operations were performed during decoding.
3. Image decoding was not performed as instructed.
4. Insufficient device memory.

**Resolution Steps**

Check the image and re-decode it following the specified instructions.

## 62980098 Shared Memory Space Error

**Error Message**

Shared memory does not exist.

**Possible Causes**

1. Insufficient memory size.
2. Out-of-bounds access to shared memory.
3. Invalid pointer usage.

**Resolution Steps**

Check memory usage or restart the device.

## 62980099 Shared Memory Data Exception

**Error Message**

Shared memory data abnormal.

**Possible Causes**

1. Synchronization operations were not performed correctly during shared memory read/write.
2. Out-of-bounds access to shared memory.
3. Invalid pointer usage.

**Resolution Steps**

Restart the device.

## 62980100 Image Decoding Error

**Error Message**

Image decoding abnormal.

**Possible Causes**

1. An exception occurred during image upload.
2. Other operations were performed during decoding.
3. Image decoding was not performed as instructed.
4. Insufficient device memory.

**Resolution Steps**

Check the image and re-decode it following the specified instructions.

## 62980101 Image Input Data Error

**Error Message**

The image data is abnormal.

**Possible Causes**

1. Incorrect image input data.
2. Incorrect image format.
3. Incorrect image size.

**Resolution Steps**

Re-enter the correct image.

## 62980102 Image Memory Allocation Error

**Error Message**

Image malloc abnormal.

**Possible Causes**

Insufficient device memory or memory is occupied.

**Resolution Steps**

Free up memory and retry.

## 62980103 Unsupported Image Type

**Error Message**

Image types are not supported.

**Possible Causes**

The type of the uploaded image is currently unsupported.

**Resolution Steps**

Retry with a different image type.

## 62980104 Image Initialization Error

**Error Message**

Image initialization abnormal.

**Possible Causes**

1. Unsupported image type.
2. Unsupported image size.
3. An error occurred during initialization.

**Resolution Steps**

Re-enter the correct parameters or replace the image.

## 62980105 Image Data Retrieval Error

**Error Message**

Image get data abnormal.

**Possible Causes**

1. The device does not support the image type.
2. Image data is missing.

**Resolution Steps**

Input a new image or check the image data.

## 62980106 Image Data Too Large

**Error Message**

The image data is too large.

**Possible Causes**

The image size is too large.

**Resolution Steps**

Replace with a smaller image.

## 62980107 Image Conversion Error

**Error Message**

Image conversion abnormal.

**Possible Causes**

1. Image conversion was abnormally terminated.
2. Incorrect encoding parameters were set.

**Resolution Steps**

Replace the image or set supported encoding parameters.

## 62980108 Image Color Conversion Error

**Error Message**

Image color conversion is abnormal.

**Possible Causes**

1. Color conversion for this image type is unsupported.
2. Device malfunction.

**Resolution Steps**

Retry or replace the image type.

## 62980109 Cropping Error

**Error Message**

Cropping exceptions.

**Possible Causes**

1. Incorrect cropping parameters.
2. Image data error.

**Resolution Steps**

Check the image data or modify the cropping parameters.

## 62980110 Image Source Data Error

**Error Message**

The image source data is abnormal.

**Possible Causes**

Image source data is missing or corrupted.

**Resolution Steps**

Check the operation steps or replace the image.

## 62980111 Incomplete Image Source Data

**Error Message**

The image source data incomplete.

**Possible Causes**

Image source data is missing.

**Resolution Steps**

Check the operation steps or replace the image.

## 62980112 Image Format Mismatch

**Error Message**

The image format does not match.

**Possible Causes**

The image format is incompatible.

**Resolution Steps**

Replace with a compatible image type.

## 62980113 Unknown Image Format

**Error Message**

Image unknown format.

**Possible Causes**

The image format is unsupported.

**Resolution Steps**

Replace the image.

## 62980114 Image Source Not Parsed

**Error Message**

Image source not parsed.

**Possible Causes**

Image source data error.

**Resolution Steps**

Check the image source data.

## 62980115 Invalid Image Parameter

**Error Message**

Invalid image parameter.

**Possible Causes**

Invalid input parameters.

**Resolution Steps**

Re-enter the correct parameters.

## 62980116 Decoding Failed

**Error Message**

Decoding failed.

**Possible Causes**

1. Decoding was abnormally terminated.
2. Unsupported image format.
3. Image was not read.

**Resolution Steps**

Check if the image was read or replace the image.

## 62980117 Plugin Registration Failed

**Error Message**

Failed to register plugin.

**Possible Causes**

1. No matching decoding or encoding plugin for the format.
2. Incorrect input data.

**Resolution Steps**

Replace the image or check the input data.

## 62980118 Plugin Creation Failed

**Error Message**

Failed to create plugin.

**Possible Causes**

1. No matching decoding or encoding plugin for the format.
2. Incorrect input data.

**Resolution Steps**

Replace the image or check the input data.

## 62980119 Image Encoding Failed

**Error Message**

Image encoding failed.

**Possible Causes**

1. Unsupported encoding format.
2. Incorrect input data.

**Resolution Steps**

Replace the image or check the input data.

## 62980120 Image Pixel Mapping Addition Failed

**Error Message**

Image addition pixel mapping failed.

**Possible Causes**

1. Pixel mapping addition may be unsupported.
2. Pixel mapping addition was abnormally terminated.

**Resolution Steps**

Check the mapping steps or replace the image.

## 62980121 Hardware Image Decoding Unsupported

**Error Message**

Image hardware decoding is not supported.

**Possible Causes**

Hardware image decoding was used.

**Resolution Steps**

Use alternative decoding methods.## 62980122 Decoding Image Header Exception

**Error Message**

Decoding image header abnormal.

**Possible Causes**

1. Abnormal termination during header decoding process.
2. Image header does not meet requirements.

**Resolution Steps**

Replace the image or verify image data integrity.

## 62980123 Image Does Not Support EXIF Decoding

**Error Message**

Image decoding exif support.

**Possible Causes**

The image does not support EXIF decoding.

**Resolution Steps**

Replace the image.

## 62980124 Image Property Does Not Exist

**Error Message**

The image property does not exist.

**Possible Causes**

1. Missing image properties.
2. Unauthorized modifications made to the image.

**Resolution Steps**

Replace the image.

## 62980133 Image Property Assignment Out of Range

**Error Message**

The EXIF data is out of range.

**Possible Causes**

Image property value exceeds valid range.

**Resolution Steps**

Replace the image or verify the range of specified image property values.

## 62980135 Invalid Image Property Value

**Error Message**

The EXIF value is invalid.

**Possible Causes**

Missing image property value.

**Resolution Steps**

Replace the image or verify image property values.

## 62980137 Invalid Image Operation

**Error Message**

Invalid media operation.

**Possible Causes**

Target image format does not support this operation.

**Resolution Steps**

Replace the image.

## 62980146 Failed to Write Image Property Value to File

**Error Message**

The EXIF data failed to be written to the file.

**Possible Causes**

Abnormal image property values.

**Resolution Steps**

Replace the image.

## 62980149 Invalid Image Parameters

**Error Message**

Invalid MIME type for the image source.

**Possible Causes**

Target image format does not support this operation.

**Resolution Steps**

Replace the image.

## 62980172 ICC Encoding Failure

**Error Message**

Failed to encode icc.

**Possible Causes**

Issues with image ICC profile information.

**Resolution Steps**

Verify image data or replace the image.

## 62980173 DMA Memory Space Error

**Error Message**

The DMA memory does not exist.

**Possible Causes**

1. Insufficient memory allocation.
2. Memory access violation.
3. Invalid pointer usage.

**Resolution Steps**

Check memory usage or restart the system.

## 62980174 DMA Memory Data Exception

**Error Message**

The DMA memory data is abnormal.

**Possible Causes**

1. Improper synchronization during shared memory read/write operations.
2. Memory access violation.
3. Invalid pointer usage.

**Resolution Steps**

Restart the system.

## 62980177 API Environment Exception

**Error Message**

Abnormal API environment.

**Possible Causes**

Issues with API runtime environment.

**Resolution Steps**

Verify SDK version compatibility.

## 62980178 PixelMap Creation Failure

**Error Message**

Failed to create the PixelMap.

**Possible Causes**

1. Parameter errors (e.g., region size exceeds limits, illegal input values) causing creation failure.
2. Premature instance release leading to creation failure.

**Resolution Steps**

Verify function parameters or check for premature instance release.

## 62980179 Abnormal Buffer Size

**Error Message**

Abnormal buffer size.

**Possible Causes**

Parameter errors (e.g., region size exceeds limits, illegal input values) causing creation failure.

**Resolution Steps**

Verify function parameters.

## 62980180 File Descriptor Mapping Failure

**Error Message**

FD mapping failed.

**Possible Causes**

Issues with provided file descriptor.

**Resolution Steps**

Verify if correct file descriptor was passed.

## 62980246 Failed to Read Pixel Map

**Error Message**

Failed to read pixel map.

**Possible Causes**

1. Corrupted pixel map data.
2. Insufficient read permissions for pixel map.

**Resolution Steps**

Recreate pixel map or modify read permissions.

## 62980247 Failed to Write Pixel Mapping

**Error Message**

Writing to pixel mapping failed.

**Possible Causes**

1. Corrupted pixel map data.
2. Insufficient write permissions for pixel map.

**Resolution Steps**

Recreate pixel map or modify write permissions.

## 62980248 PixelMap Modification Not Allowed

**Error Message**

PixelMap does not allow modification.

**Possible Causes**

Unauthorized modifications made to PixelMap.

**Resolution Steps**

Discontinue PixelMap modifications.

## 62980252 Surface Creation Failure

**Error Message**

Failed to create surface.

**Possible Causes**

Memory allocation error during image encoding.

**Resolution Steps**

Retry operation or replace the image.

## 62980259 Configuration Error

**Error Message**

Configuration error.

**Possible Causes**

Incorrect configuration settings.

**Resolution Steps**

Reconfigure with correct parameters.

## 62980274 Image Conversion Failure

**Error Message**

The conversion failed.

**Possible Causes**

1. Abnormal termination during image conversion.
2. Incorrect encoding parameter settings.

**Resolution Steps**

Replace the image or configure supported encoding parameters.

## 62980276 Unsupported Target Conversion Type

**Error Message**

The type to be converted is an unsupported target pixel format.

**Possible Causes**

Target conversion type is not supported.

**Resolution Steps**

Replace the image or select alternative conversion type.

## 62980286 PixelMap Memory Identifier Setting Failure

**Error Message**

Memory format not supported.

**Possible Causes**

1. PixelMap memory type mismatch.
2. Invalid PixelMap file descriptor.
3. Unknown kernel error.

**Resolution Steps**

Verify PixelMap instance release status. Check memory type compatibility.

## 62980302 Memory Copy Failure

**Error Message**

Memory copy failed.

**Possible Causes**

1. Memory type mismatch.
2. Invalid file descriptor.
3. Unknown kernel error.

**Resolution Steps**

Verify instance release status for copying. Check memory type compatibility.

## 7600201 Unsupported Operation

**Error Message**

Unsupported operation.

**Possible Causes**

Operation is not supported.

**Resolution Steps**

Use supported operations.

## 7600202 Unsupported Metadata Read/Write

**Error Message**

Unsupported metadata. Possible causes: Unsupported metadata type.

**Possible Causes**

Unsupported metadata operations, such as:
- Unsupported EXIF fields
- Mismatched auxiliary image types
- Attempting to retrieve specific auxiliary image metadata (e.g., requesting GainmapMetadata from depth map)

**Resolution Steps**

Verify auxiliary image type and metadata type compatibility before performing operations.

## 7600301 Memory Allocation Failure

**Error Message**

Memory alloc failed.

**Possible Causes**

Insufficient device memory or memory contention.

**Resolution Steps**

Free up memory and retry.

## 7600302 Memory Copy Failure

**Error Message**

Memory copy failed.

**Possible Causes**

1. Target memory for copying does not exist.
2. Insufficient device memory.

**Resolution Steps**

Verify existence of target memory. Free up memory and retry.## 7600901 Unknown Error

**Error Message**

Unknown error.

**Possible Causes**

Error caused by unknown reasons.

**Resolution Steps**

Investigate the cause through logs.

## 7700101 Invalid Image Source

**Error Message**

Bad source.

**Possible Causes**

1. The device does not support this image type.  
2. Image decoding was not performed as instructed.

**Resolution Steps**

Check image data or replace the image.

## 7700102 Unsupported MIME Type

**Error Message**

Unsupported mimetype.

**Possible Causes**

The device does not support this image type.

**Resolution Steps**

Check image data or replace the image.

## 7700103 Image Too Large

**Error Message**

Image too large.

**Possible Causes**

The image size exceeds the limit.

**Resolution Steps**

Check image data or replace the image.

## 7700201 Unsupported Allocator Type

**Error Message**

Unsupported allocator type, e.g., use share memory to decode a HDR image as only DMA supported hdr metadata.

**Possible Causes**

The memory allocator type was not specified or an incorrect type was specified. For example: Using shared memory to decode an HDR image will cause an error because only DMA supports HDR metadata.

**Resolution Steps**

Use the correct memory allocator type.

## 7700203 Unsupported Options

**Error Message**

Unsupported options, e.g, cannot convert image into desired pixel format.

**Possible Causes**

Some option parameters are incorrectly configured, and the operation required by the option is not supported.

**Resolution Steps**

Check option parameter configurations.

## 7700301 Decoding Failed

**Error Message**

Decode failed.

**Possible Causes**

1. Insufficient device memory.  
2. The device does not support this image type.  
3. Image decoding was not performed as instructed.

**Resolution Steps**

Check image data or replace the image.

## 7700302 Memory Allocation Failed

**Error Message**

Memory allocation failed.

**Possible Causes**

1. Insufficient device memory.  
2. Image decoding was not performed as instructed.

**Resolution Steps**

Check device memory or verify input data.

## 7800201 Unsupported Options

**Error Message**

Unsupported options.

**Possible Causes**

Some option parameters are incorrectly configured, and the operation required by the option is not supported.

**Resolution Steps**

Check option parameter configurations.

## 7800301 Encoding Failed

**Error Message**

Encode failed.

**Possible Causes**

1. The specified encoding format is not supported.  
2. Incorrect input data was provided.

**Resolution Steps**

Replace the image or check input data.