# Editing Image EXIF Information

The image tool currently provides capabilities for reading and editing EXIF information of images.

EXIF (Exchangeable Image File Format) is a file format specifically designed for digital camera photos, which can record attribute information and shooting data of digital photos. Currently, only JPEG format images are supported.

In applications such as photo galleries, there is a need to view or modify the EXIF information of digital photos. Since parameters from manual camera lenses cannot be automatically written to EXIF information or shooting time errors frequently occur due to camera power loss, manual correction of incorrect EXIF data becomes necessary. This functionality can be utilized for such purposes.

OpenHarmony currently supports viewing and modifying only certain EXIF information. For the specific supported range, please refer to: [Exif Information](../../../../en/application-dev/reference/ImageKit/cj-apis-image.md#enum-propertykey).

## Development Steps

For detailed information on the APIs related to reading and editing EXIF information, please refer to the [API Reference](../../../../en/application-dev/reference/ImageKit/cj-apis-image.md#func-getimagepropertypropertykey-imagepropertyoptions).

1. Obtain the image and create an ImageSource.

   <!-- compile -->

   ```cangjie
   // Import the relevant module packages.
   import kit.ImageKit.*

   // Obtain the sandbox path to create an ImageSource.
   let fd : Int32 = 0 // Obtain the fd of the image to be processed.
   let imageSourceApi = createImageSource(fd)
   ```

2. Read and edit EXIF information.

    <!-- compile -->

   ```cangjie
    // Read EXIF information, where BitsPerSample represents the number of bits per pixel.
    let options : ImagePropertyOptions = ImagePropertyOptions(index: 0, defaultValue: '9999')
    let data = imageSourceApi.getImageProperty(PropertyKey.BITS_PER_SAMPLE, options: options)

    // Edit EXIF information.
    imageSourceApi.modifyImageProperty(PropertyKey.IMAGE_WIDTH, "120")
    ```