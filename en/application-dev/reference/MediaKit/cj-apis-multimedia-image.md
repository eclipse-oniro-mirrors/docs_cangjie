# ohos.multimedia.image

This module provides image processing capabilities, including creating PixelMap through properties, reading image pixel data, and reading image data within a specified region.

## Importing the Module

```cangjie
import kit.ImageKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample projects and configuration templates, please refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class ImageReceiver

```cangjie
public class ImageReceiver {}
```

**Description:** The ImageReceiver class is used to obtain component surface IDs, receive the latest image, read the next image, and release the ImageReceiver instance.

An ImageReceiver instance must be created before calling the following methods.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

### func off(ReceiveType)

```cangjie
public func off(eventType: ReceiveType): Unit
```

**Description:** Removes the registered callback when releasing the buffer.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

**Parameters:**

| Name      | Type                                                         | Mandatory | Default | Description                                                                 |
| :-------- | :----------------------------------------------------------- | :-------- | :------ | :-------------------------------------------------------------------------- |
| eventType | [ReceiveType](../ImageKit/cj-apis-image.md#enum-receivetype) | Yes       | -       | The type of registered event, fixed as 'imageArrival', triggered when releasing the buffer. |

### func on(ReceiveType, Callback0Argument)

```cangjie
public func on(eventType: ReceiveType, callback: Callback0Argument): Unit
```

**Description:** Registers a callback when receiving an image.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

**Parameters:**

| Name      | Type                                                                 | Mandatory | Default | Description                                                                 |
| :-------- | :------------------------------------------------------------------- | :-------- | :------ | :-------------------------------------------------------------------------- |
| eventType | [ReceiveType](../ImageKit/cj-apis-image.md#enum-receivetype)         | Yes       | -       | The type of registered event, fixed as 'imageArrival', triggered when receiving an image. |
| callback  | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes       | -       | The callback function. If the registration event is triggered successfully, err is undefined; otherwise, it is an error object. |

### func readLatestImage()

```cangjie
public func readLatestImage(): Image
```

**Description:** Reads the latest image from the ImageReceiver.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

**Return Value:**

| Type                              | Description          |
| :-------------------------------- | :------------------- |
| [Image](../ImageKit/cj-apis-image.md#class-image) | Returns the latest image. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Image Error Codes](../ImageKit/cj-errorcode-image.md).

  | Error Code ID | Error Message                          |
  | :----------- | :------------------------------------- |
  | 62980104     | Failed to initialize the internal object. |

### func readNextImage()

```cangjie
public func readNextImage(): Image
```

**Description:** Reads the next image from the ImageReceiver.

**System Capability:** SystemCapability.Multimedia.Image.ImageReceiver

**Since:** 21

**Return Value:**

| Type                              | Description          |
| :-------------------------------- | :------------------- |
| [Image](../ImageKit/cj-apis-image.md#class-image) | The next image. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Image Error Codes](../ImageKit/cj-errorcode-image.md).

  | Error Code ID | Error Message                          |
  | :----------- | :------------------------------------- |
  | 62980104     | Failed to initialize the internal object. |