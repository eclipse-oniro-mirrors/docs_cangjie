# Using ImageSource for Image Decoding

Image decoding refers to the process of converting archived images in supported formats into a unified [PixelMap](./cj-image-overview.md) for image display or [image processing](./cj-image-transformation.md) within applications or systems. Currently supported archived image formats include JPEG, PNG, GIF, WebP, BMP, SVG, ICO, DNG, and HEIF (availability may vary across different hardware devices).

## Development Steps

For detailed API documentation on image decoding, refer to: [Image Decoding API Reference](../../../../en/application-dev/reference/ImageKit/cj-apis-image.md#class-imagesource).

1. Import the Image module globally.

    <!-- compile -->

    ```cangjie
    import kit.ImageKit.*
    ```

2. Obtain the image.
    - Method 1: Get the file descriptor through the sandbox path. Refer to the [file.fs API documentation](../../../../en/application-dev/reference/CoreFileKit/cj-apis-file_fs.md).
       This method requires importing the kit.CoreFileKit and kit.AbilityKit modules first.

        <!-- compile -->

        ```cangjie
        import kit.CoreFileKit.*
        import kit.AbilityKit.*
        ```

        Then call FileFs.open() to obtain the file descriptor.

        <!-- compile -->

        ```cangjie
        let cacheDir = "/data/storage/el2/base/haps/entry/cache"
        let filePath = cacheDir + '/test.jpg'
        let file = FileIo.open(filePath, mode: OpenMode.READ_WRITE)
        let fd = file.fd 
        ```

    - Method 2: Get the resource file's Array\<UInt8> through the resource manager. Refer to the [ResourceManager API documentation](../../../../en/application-dev/reference/LocalizationKit/cj-apis-resource_manager.md#func-getrawfilecontentstring).

        <!-- compile -->

        ```cangjie
        // Import the resourceManager.
        import kit.LocalizationKit.*
        import ohos.hilog.Hilog

        var abilityContext = Global.abilityContext
        // Get the resourceManager.
        let resourceManager = abilityContext.resourceManager
        ```

        Different models may have different ways to obtain the resource manager. After obtaining it, call getRawFileContent() to get the resource file's Array\<UInt8>.

        <!-- compile -->

        ```cangjie
        try {
          let buffer = resourceManager.getRawFileContent("test.jpg")
        } catch (e: BusinessException) {
          Hilog.error(0, "Failed to get RawFileContent", e.message)
        }
        ```

    - Method 4: Get the resource file's RawFileDescriptor through the resource manager. Refer to the [ResourceManager API documentation](../../../../en/application-dev/reference/LocalizationKit/cj-apis-resource_manager.md#func-getrawfdstring).

        <!-- compile -->

        ```cangjie
        // Import the resourceManager.
        import kit.LocalizationKit.*

        var abilityContext = Global.abilityContext
        // Get the resourceManager.
        let resourceManager = abilityContext.resourceManager
        ```

        Different models may have different ways to obtain the resource manager. After obtaining it, call getRawFd() to get the resource file's RawFileDescriptor.

        <!-- compile -->

        ```cangjie
        try {
          let rawFileDescriptor = resourceManager.getRawFd("test.jpg")
        } catch (e: BusinessException) {
          Hilog.error(0, "Failed to get RawFileContent", e.message)
        }
        ```

3. Create an ImageSource instance.

    - Method 1: Create ImageSource through the sandbox path. The sandbox path can be obtained via Method 1 in Step 2.

        <!-- compile -->

        ```cangjie
        // filePath is the obtained sandbox path.
        let imageSource = createImageSource(filePath)
        ```

    - Method 2: Create ImageSource through the file descriptor fd. The file descriptor can be obtained via Method 2 in Step 2.

        <!-- compile -->

        ```cangjie
        // fd is the obtained file descriptor.
        let imageSource = createImageSource(fd)
        ```

    - Method 3: Create ImageSource through the buffer array. The buffer array can be obtained via Method 3 in Step 2.

        <!-- compile -->

        ```cangjie
        let imageSource = createImageSource(buffer)
        ```

    - Method 4: Create ImageSource through the resource file's RawFileDescriptor. The RawFileDescriptor can be obtained via Method 4 in Step 2.

        <!-- compile -->

        ```cangjie
        let imageSource = createImageSource(rawFileDescriptor);
        ```

4. Set the decoding parameters (DecodingOptions) and decode to obtain the pixelMap image object.
    - Decode with the desired format:

        <!-- compile -->

        ```cangjie
        import kit.ImageKit.*
        import kit.AbilityKit.*
        import ohos.resource_manager.AppResource

        var abilityContext = Global.abilityContext
        // Get the resourceManager.
        let resourceManager = abilityContext.resourceManager

        let img = resourceManager.getMediaContent(@r(app.media.layered_image))
        let imageSource = createImageSource(img)
        let decodingOptions = DecodingOptions(editable: true, desiredPixelFormat: PixelMapFormat.Rgba8888)

        // Create pixelMap.
        let pixelMap = imageSource.createPixelMap(options: decodingOptions)
        ```

    - HDR Image Decoding

        <!-- compile -->

        ```cangjie
        import kit.ImageKit.*
        import kit.AbilityKit.*
        import ohos.resource_manager.AppResource

        var abilityContext = Global.abilityContext
        // Get the resourceManager.
        let resourceManager = abilityContext.resourceManager

        let img = resourceManager.getMediaContent(@r(app.media.layered_image))
        let imageSource = createImageSource(img)
        // Setting to AUTO will decode based on the image resource format. If the resource is HDR, it will decode to an HDR pixelmap.
        let decodingOptions = DecodingOptions(desiredDynamicRange: DecodingDynamicRange.Auto)

        // Create pixelMap.
        let pixelMap = imageSource.createPixelMap(options: decodingOptions)
        // Check if the pixelmap contains HDR content.
        let info = pixelMap.getImageInfo()
        ```

    After decoding is complete and the pixelMap object is obtained, you can proceed with subsequent [image processing](./cj-image-transformation.md).

5. Release pixelMap and imageSource.

    Ensure that all pixelMap and imageSource operations are completed. When these variables are no longer needed, manually call the following methods to release them as required.

    <!-- compile -->

    ```cangjie
    pixelMap.release();
    imageSource.release();
    ```

## Development Example - Decoding an Image from Resource Files

1. Obtain the resourceManager.

    <!-- compile -->

    ```cangjie
    // Import the resourceManager.
    import kit.LocalizationKit.*
    import kit.AbilityKit.*

    // globalcontext needs to be assigned in func onCreate of main_ability.cj: globalcontext = this.context
    var abilityContext = Global.abilityContext
    // Get the resourceManager.
    let resourceManager = abilityContext.resourceManager
    ```

2. Create ImageSource.
    - Method 1: Create through Array\<UInt8> of test.jpg in the rawfile folder.

        <!-- compile -->

        ```cangjie
        let buffer = resourceManager.getRawFileContent("test.jpg")
        let imageSource = createImageSource(buffer)
        ```

    - Method 2: Create through RawFileDescriptor of test.jpg in the rawfile folder.

        <!-- compile -->

        ```cangjie
        let rawFileDescriptor = resourceManager.getRawFd("test.jpg")
        let imageSource = createImageSource(rawFileDescriptor)
        ```

3. Create pixelMap.

    <!-- compile -->

    ```cangjie
    let pixelMap = imageSource.createPixelMap()
    ```

4. Release pixelMap and imageSource.

    Ensure that all pixelMap and imageSource operations are completed. When these variables are no longer needed, manually call the following methods to release them as required.

    <!-- compile -->

    ```cangjie
    pixelMap.release();
    imageSource.release();
    ```