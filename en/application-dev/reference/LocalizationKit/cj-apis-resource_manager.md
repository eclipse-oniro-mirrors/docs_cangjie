# ohos.resource_manager

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The resource management module provides interfaces for obtaining application resource objects based on the current configuration: language, region, screen orientation (portrait/landscape), MCC (Mobile Country Code), MNC (Mobile Network Code), device capability (device type), and screen density.

## Import Module

```cangjie
import kit.LocalizationKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Example Code Description](../cj-development-intro.md#仓颉示例代码说明).

## class Configuration

```cangjie
public class Configuration {
    public var direction: Direction
    public var locale: String
    public var deviceType: DeviceType
    public var screenDensity: ScreenDensity
    public var colorMode: ColorMode
    public var mcc: UInt32
    public var mnc: UInt32
}
```

**Function:** Represents the configuration of the current device.

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

### var colorMode

```cangjie
public var colorMode: ColorMode
```

**Function:** Color mode.

**Type:** [ColorMode](#enum-colormode)

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

### var deviceType

```cangjie
public var deviceType: DeviceType
```

**Function:** Device type.

**Type:** [DeviceType](#enum-devicetype)

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

### var direction

```cangjie
public var direction: Direction
```

**Function:** Screen orientation.

**Type:** [Direction](#enum-direction)

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

### var locale

```cangjie
public var locale: String
```

**Function:** Language, script, country, and region.

**Type:** String

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

### var mcc

```cangjie
public var mcc: UInt32
```

**Function:** Mobile Country Code.

**Type:** UInt32

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

### var mnc

```cangjie
public var mnc: UInt32
```

**Function:** Mobile Network Code.

**Type:** UInt32

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

### var screenDensity

```cangjie
public var screenDensity: ScreenDensity
```

**Function:** Screen density.

**Type:** [ScreenDensity](#enum-screendensity)

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

## class DeviceCapability

```cangjie
public class DeviceCapability {
    public var screenDensity: ScreenDensity
    public var deviceType: DeviceType
}
```

**Function:** Represents the capabilities supported by the device.

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

### var deviceType

```cangjie
public var deviceType: DeviceType
```

**Function:** Current device type.

**Type:** [DeviceType](#enum-devicetype)

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

### var screenDensity

```cangjie
public var screenDensity: ScreenDensity
```

**Function:** Current device screen density.

**Type:** [ScreenDensity](#enum-screendensity)

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

## class ResourceManager

```cangjie
public class ResourceManager {}
```

**Function:** Provides the capability to access application resources.

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

### func addResource(String)

```cangjie
public func addResource(path: String): Unit
```

**Function:** During application runtime, loads the specified resource path to implement resource overlay.

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Resource path. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001010 | Invalid overlay path. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let path = "/data/storage/el2/base/haps/entry/files/library-default-unsigned.hsp"
    resourceManager.addResource(path)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func closeRawFd(String)

```cangjie
public func closeRawFd(path: String): Unit
```

**Function:** Closes a rawfile file in the resources/rawfile directory.

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Rawfile file path. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001005 | The resource not found by path. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let rawfd = resourceManager.closeRawFd("test.txt")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getBoolean(UInt32)

```cangjie
public func getBoolean(resId: UInt32): Bool
```

**Function:** Gets the boolean result corresponding to the resource ID.

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resId | UInt32 | Yes | - | Resource ID. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Boolean result corresponding to the resource object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |
  | 9001006 | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.boolean.test)
    resourceManager.getBoolean(res.id)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getBoolean(AppResource)

```cangjie
public func getBoolean(resource: AppResource): Bool
```

**Function:** Gets the boolean result corresponding to the resource object. This interface is used for cross-package access within multi-project applications.

**System Capability:** SystemCapability.Global.ResourceManager

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resource | [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource) | Yes | - | Resource object. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Boolean result corresponding to the resource object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |
  | 9001006 | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.boolean.test)
    let resource = AppResource("com.example.myapplication", "entry", res.id)
    resourceManager.getBoolean(resource)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func getBooleanByName(String)

```cangjie
public func getBooleanByName(resName: String): Bool
```

**Function:** Retrieves the boolean value corresponding to the resource name.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter Name | Type   | Mandatory | Default Value | Description          |
|:---------------|:-------|:----------|:--------------|:---------------------|
| resName        | String | Yes       | -             | The resource name.   |

**Return Value:**

| Type | Description                          |
|:-----|:-------------------------------------|
| Bool | The boolean value corresponding to the resource name. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message                        |
  |:-------------|:-------------------------------------|
  | 9001003      | Invalid resource name.               |
  | 9001004      | No matching resource is found based on the resource name. |
  | 9001006      | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message         | Possible Cause | Handling Steps |
  |:---------------------|:---------------|:---------------|
  | If the instance id invalid. | todo           | todo           |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    resourceManager.getBooleanByName("test")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getColor(AppResource)

```cangjie
public func getColor(resource: AppResource): UInt32
```

**Function:** Retrieves the color value corresponding to the resource object. This interface is used for cross-package access within multi-project applications.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter Name | Type                              | Mandatory | Default Value | Description          |
|:---------------|:----------------------------------|:----------|:--------------|:---------------------|
| resource       | [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource) | Yes       | -             | The resource object. |

**Return Value:**

| Type   | Description                          |
|:-------|:-------------------------------------|
| UInt32 | The color value corresponding to the resource object (in decimal). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message                        |
  |:-------------|:-------------------------------------|
  | 9001001      | Invalid resource ID.                 |
  | 9001002      | No matching resource is found based on the resource ID. |
  | 9001006      | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message         | Possible Cause | Handling Steps |
  |:---------------------|:---------------|:---------------|
  | If the instance id invalid. | todo           | todo           |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.color.test)
    let resource = AppResource("com.example.myapplication", "entry", res.id)
    resourceManager.getColor(resource)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getColor(UInt32)

```cangjie
public func getColor(resId: UInt32): UInt32
```

**Function:** Retrieves the color value corresponding to the resource ID.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter Name | Type   | Mandatory | Default Value | Description          |
|:---------------|:-------|:----------|:--------------|:---------------------|
| resId          | UInt32 | Yes       | -             | The resource ID.     |

**Return Value:**

| Type   | Description                          |
|:-------|:-------------------------------------|
| UInt32 | The color value corresponding to the resource ID (in decimal). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message                        |
  |:-------------|:-------------------------------------|
  | 9001001      | Invalid resource ID.                 |
  | 9001002      | No matching resource is found based on the resource ID. |
  | 9001006      | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message         | Possible Cause | Handling Steps |
  |:---------------------|:---------------|:---------------|
  | If the instance id invalid. | todo           | todo           |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.color.test)
    resourceManager.getColor(res.id)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getColorByName(String)

```cangjie
public func getColorByName(resName: String): UInt32
```

**Function:** Retrieves the color value corresponding to the resource name.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter Name | Type   | Mandatory | Default Value | Description          |
|:---------------|:-------|:----------|:--------------|:---------------------|
| resName        | String | Yes       | -             | The resource name.   |

**Return Value:**

| Type   | Description                          |
|:-------|:-------------------------------------|
| UInt32 | The color value corresponding to the resource name (in decimal). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message                        |
  |:-------------|:-------------------------------------|
  | 9001003      | Invalid resource name.               |
  | 9001004      | No matching resource is found based on the resource name. |
  | 9001006      | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message         | Possible Cause | Handling Steps |
  |:---------------------|:---------------|:---------------|
  | If the instance id invalid. | todo           | todo           |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    resourceManager.getColorByName("test")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getConfiguration()

```cangjie
public func getConfiguration(): Configuration
```

**Function:** Retrieves the device configuration information and returns a [Configuration](#class-configuration) object.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Return Value:**

| Type                              | Description                          |
|:----------------------------------|:-------------------------------------|
| [Configuration](#class-configuration) | The device configuration information. |

**Exceptions:**

- IllegalStateException:

  | Error Message         | Possible Cause | Handling Steps |
  |:---------------------|:---------------|:---------------|
  | If the instance id invalid. | todo           | todo           |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let configuration = resourceManager.getConfiguration()
    Hilog.info(0, "test", configuration.locale, "")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getDeviceCapability()

```cangjie
public func getDeviceCapability(): DeviceCapability
```

**Function:** Retrieves the device capability and returns a [DeviceCapability](#class-devicecapability) object.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Return Value:**

| Type                                  | Description                          |
|:--------------------------------------|:-------------------------------------|
| [DeviceCapability](#class-devicecapability) | The device capability.               |

**Exceptions:**

- IllegalStateException:

  | Error Message         | Possible Cause | Handling Steps |
  |:---------------------|:---------------|:---------------|
  | If the instance id invalid. | todo           | todo           |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let deviceCapability = resourceManager.getDeviceCapability()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getLocales(Bool)

```cangjie
public func getLocales(includeSystem!: Bool = false): Array<String>
```

**Function:** Retrieves the list of languages supported by the application.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter Name | Type | Mandatory | Default Value | Description          |
|:---------------|:-----|:----------|:--------------|:---------------------|
| includeSystem  | Bool | No        | false         | **Named parameter.** Whether to include system resources. Default is false. <br> false: Only retrieves the language list of application resources. <br> true: Retrieves the language list of both system and application resources. <br> When retrieving the language list for system resource management objects, the includeSystem value is ignored, and the system resource language list is returned. |

**Return Value:**

| Type          | Description                          |
|:--------------|:-------------------------------------|
| Array\<String> | Returns the retrieved language list. Strings in the list are composed of language, script (optional), and region (optional), concatenated in order with hyphens "-". |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message                        |
  |:-------------|:-------------------------------------|
  | 401          | If the input parameter is invalid. Possible causes: Incorrect parameter types. |

- IllegalStateException:

  | Error Message         | Possible Cause | Handling Steps |
  |:---------------------|:---------------|:---------------|
  | If the instance id invalid. | todo           | todo           |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    resourceManager.getLocales()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getMediaBase64ByName(String, ?ScreenDensity)

```cangjie
public func getMediaBase64ByName(resName: String, density!: ?ScreenDensity = None): String
```

**Function:** Retrieves the image resource corresponding to the resource name for the specified screen density and returns the Base64 encoding of the image resource.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter Name | Type                          | Mandatory | Default Value | Description          |
|:---------------|:------------------------------|:----------|:--------------|:---------------------|
| resName        | String                        | Yes       | -             | The resource ID.     |
| density        | ?[ScreenDensity](#enum-screendensity) | No        | None          | **Named parameter.** The screen density required for resource retrieval. 0 or omitted means the default screen density. |

**Return Value:**

| Type   | Description                          |
|:-------|:-------------------------------------|
| String | The Base64 encoding of the image resource corresponding to the resource name. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message                        |
  |:-------------|:-------------------------------------|
  | 9001003      | Invalid resource name.               |
  | 9001004      | No matching resource is found based on the resource name. |

- IllegalStateException:

  | Error Message         | Possible Cause | Handling Steps |
  |:---------------------|:---------------|:---------------|
  | If the instance id invalid. | todo           | todo           |

- IllegalMemoryException:

  | Error Message         | Possible Cause | Handling Steps |
  |:---------------------|:---------------|:---------------|
  | Out of memory.       | todo           | todo           |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    resourceManager.getMediaBase64ByName("test")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func getMediaByName(String, ?ScreenDensity)

```cangjie
public func getMediaByName(resName: String, density!: ?ScreenDensity = None): Array<UInt8>
```

**Function:** Retrieves the media file content corresponding to the specified resource name and screen density.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| resName | String | Yes | - | Resource name. |
| density | ?[ScreenDensity](#enum-screendensity) | No | None | The screen density required for resource retrieval, where 0 indicates the default screen density. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt8> | The media resource corresponding to the resource name. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001003 | Invalid resource name. |
  | 9001004 | No matching resource is found based on the resource name. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    resourceManager.getMediaByName("test", density: ScreenMdpi)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getMediaContent(UInt32, ?ScreenDensity)

```cangjie
public func getMediaContent(resId: UInt32, density!: ?ScreenDensity = None): Array<UInt8>
```

**Function:** Retrieves the media file content corresponding to the specified resource ID and screen density.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| resId | UInt32 | Yes | - | Resource ID. |
| density | ?[ScreenDensity](#enum-screendensity) | No | None | The screen density required for resource retrieval, where 0 indicates the default screen density. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt8> | The media resource corresponding to the resource ID. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.media.test)
    resourceManager.getMediaContent(res.id, density: ScreenSdpi)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getMediaContent(AppResource, ?ScreenDensity)

```cangjie
public func getMediaContent(resource: AppResource, density!: ?ScreenDensity = None): Array<UInt8>
```

**Function:** Retrieves the media file content corresponding to the specified resource object and screen density. This interface is used for cross-package access in multi-project applications.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| resource | [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource) | Yes | - | Resource object. |
| density | ?[ScreenDensity](#enum-screendensity) | No | None | The screen density required for resource retrieval, where 0 indicates the default screen density. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt8> | The media resource corresponding to the resource object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.media.test)
    let resource = AppResource("com.example.myapplication", "entry", res.id)
    resourceManager.getMediaContent(resource, density: ScreenSdpi)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getMediaContentBase64(UInt32, ?ScreenDensity)

```cangjie
public func getMediaContentBase64(resId: UInt32, density!: ?ScreenDensity = None): String
```

**Function:** Retrieves the image resource corresponding to the specified resource ID and screen density, returning the Base64 encoding of the image resource.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| resId | UInt32 | Yes | - | Resource ID. |
| density | ?[ScreenDensity](#enum-screendensity) | No | None | **Named parameter.** The screen density required for resource retrieval, where 0 or omission indicates the default screen density. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | The Base64 encoding of the image resource corresponding to the resource ID. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

- IllegalMemoryException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | Out of memory. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.media.test)
    resourceManager.getMediaContentBase64(res.id)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getMediaContentBase64(AppResource, ?ScreenDensity)

```cangjie
public func getMediaContentBase64(resource: AppResource, density!: ?ScreenDensity = None): String
```

**Function:** Retrieves the image resource corresponding to the specified resource object and screen density, returning the Base64 encoding of the image resource. This interface is used for cross-package access in multi-project applications.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| resource | [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource) | Yes | - | Resource object. |
| density | ?[ScreenDensity](#enum-screendensity) | No | None | **Named parameter.** The screen density required for resource retrieval, where 0 or omission indicates the default screen density. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | The Base64 encoding of the image resource corresponding to the resource object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

- IllegalMemoryException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | Out of memory. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.media.test)
    let resource = AppResource("com.example.myapplication", "entry", res.id)
    resourceManager.getMediaContentBase64(resource)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getNumber(UInt32)

```cangjie
public func getNumber(resId: UInt32): NumberValueType
```

**Function:** Retrieves the numeric resource corresponding to the specified resource ID.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| resId | UInt32 | Yes | - | Resource ID. |

**Return Value:**

| Type | Description |
|:----|:----|
| [NumberValueType](#enum-numbervaluetype) | The numeric resource corresponding to the resource object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |
  | 9001006 | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import kit.PerformanceAnalysisKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.integer.test)
    let number = resourceManager.getNumber(res.id)
    match (number) {
        case Int32Value(v) => Hilog.info(0, "test", v.toString(), "")
        case Float32Value(v) => Hilog.info(0, "test", v.toString(), "")
        case _ => throw IllegalArgumentException("The type is not supported.")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getNumber(AppResource)

```cangjie
public func getNumber(resource: AppResource): NumberValueType
```

**Function:** Retrieves the numeric resource corresponding to the specified resource object. This interface is used for cross-package access in multi-project applications.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| resource | [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource) | Yes | - | Resource object. |

**Return Value:**

| Type | Description |
|:----|:----|
| [NumberValueType](#enum-numbervaluetype) | The numeric resource corresponding to the resource object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |
  | 9001006 | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import kit.PerformanceAnalysisKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.integer.test)
    let resource = AppResource("com.example.myapplication", "entry", res.id)
    let number = resourceManager.getNumber(resource)
    match (number) {
        case Int32Value(v) => Hilog.info(0, "test", v.toString(), "")
        case Float32Value(v) => Hilog.info(0, "test", v.toString(), "")
        case _ => throw IllegalArgumentException("The type is not supported.")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func getNumberByName(String)

```cangjie
public func getNumberByName(resName: String): NumberValueType
```

**Function:** Retrieves the numeric resource corresponding to the resource name. If both integer and float resources share the same `resName`, the integer resource value is prioritized.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resName | String | Yes | - | Resource name. |

**Return Value:**

| Type | Description |
|:----|:----|
| [NumberValueType](#enum-numbervaluetype) | Numeric resource corresponding to the resource name. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001003 | Invalid resource name. |
  | 9001004 | No matching resource is found based on the resource name. |
  | 9001006 | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import kit.PerformanceAnalysisKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let number = resourceManager.getNumberByName("test")
    match (number) {
        case Int32Value(v) => Hilog.info(0, "test", v.toString(), "")
        case Float32Value(v) => Hilog.info(0, "test", v.toString(), "")
        case _ => throw IllegalArgumentException("The type is not supported.")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getPluralStringByName(String, Int64)

```cangjie
public func getPluralStringByName(resName: String, num: Int64): String
```

**Function:** Retrieves the plural string resource corresponding to the resource name and formats the string based on the specified quantity.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resName | String | Yes | - | Resource name. |
| num | Int64 | Yes | - | Quantity value. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Plural string resource corresponding to the specified resource name. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001003 | Invalid resource name. |
  | 9001004 | No matching resource is found based on the resource name. |
  | 9001006 | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

- IllegalMemoryException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | Out of memory. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    resourceManager.getPluralStringByName("test", 1)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getPluralStringValue(UInt32, Int64)

```cangjie
public func getPluralStringValue(resId: UInt32, num: Int64): String
```

**Function:** Retrieves the plural string resource corresponding to the resource ID and formats the string based on the specified quantity.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resId | UInt32 | Yes | - | Resource ID. |
| num | Int64 | Yes | - | Quantity value. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Plural string resource corresponding to the specified resource object. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |
  | 9001006 | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

- IllegalMemoryException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | Out of memory. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.plural.test)
    resourceManager.getPluralStringValue(res.id, 1)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getPluralStringValue(AppResource, Int64)

```cangjie
public func getPluralStringValue(resource: AppResource, num: Int64): String
```

**Function:** Retrieves the plural string resource corresponding to the resource object and formats the string based on the specified quantity. This interface is used for cross-package access in multi-project applications.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resource | [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource) | Yes | - | Resource object. |
| num | Int64 | Yes | - | Quantity value. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Plural string resource corresponding to the specified resource object. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |
  | 9001006 | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

- IllegalMemoryException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | Out of memory. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.plural.test)
    let resource = AppResource("com.example.myapplication", "entry", res.id)
    resourceManager.getPluralStringValue(resource, 1)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getRawFd(String)

```cangjie
public func getRawFd(path: String): RawFileDescriptor
```

**Function:** Retrieves the descriptor of the rawfile file corresponding to the specified path in the resources/rawfile directory.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Path of the rawfile file. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RawFileDescriptor](./cj-apis-raw_file_descriptor.md#class-rawfiledescriptor) | Descriptor of the rawfile file. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001005 | Invalid relative path. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let rawfd = resourceManager.getRawFd("test.txt")
    Hilog.info(0, "test", "${rawfd.fd} ${rawfd.offset} ${rawfd.length}", "")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getRawFileContent(String)

```cangjie
public func getRawFileContent(path: String): Array<UInt8>
```

**Function:** Retrieves the content of the rawfile file corresponding to the specified path in the resources/rawfile directory, returning a byte array.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Path of the rawfile file. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt8> | Content of the rawfile file. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001005 | Invalid relative path. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    resourceManager.getRawFileContent("test.txt")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getRawFileList(String)

```cangjie
public func getRawFileList(path: String): Array<String>
```

**Function:** Retrieves the list of folders and files in the resources/rawfile directory, returning a string array of the file list.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Path of the rawfile folder. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | List of items in the rawfile folder (including subfolders and files). |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001005 | Invalid relative path. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    resourceManager.getRawFileList("")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func getString(UInt32, Array\<ArgsValueType>)

```cangjie
public func getString(resId: UInt32, args: Array<ArgsValueType>): String
```

**Function:** Retrieves the string resource corresponding to the resource ID and formats it based on the args parameters.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resId | UInt32 | Yes | - | Resource object. |
| args | Array\<[ArgsValueType](#enum-argsvaluetype)> | Yes | - | Parameters for formatting the string resource. <br>Supported parameter types: <br /> %d, %f, %s, %%. <br>Note: %% is an escape character that translates to %. <br>Example: %%d will be formatted as the string %d. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | The formatted string corresponding to the resource name. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 9001001 | Invalid resource ID. |
| 9001002 | No matching resource is found based on the resource ID. |
| 9001006 | The resource is referenced cyclically. |
| 9001007 | Failed to format the resource obtained based on the resource ID. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let resource = @r(app.string.test)
    resourceManager.getString(resource.id)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getString(AppResource, Array\<ArgsValueType>)

```cangjie
public func getString(resource: AppResource, args: Array<ArgsValueType>): String
```

**Function:** Retrieves the string resource corresponding to the resource object and formats it based on the args parameters.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resource | [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource) | Yes | - | Resource object. |
| args | Array\<[ArgsValueType](#enum-argsvaluetype)> | Yes | - | Parameters for formatting the string resource. <br>Supported parameter types: <br /> %d, %f, %s, %%. <br>Note: %% is an escape character that translates to %. <br>Example: %%d will be formatted as the string %d. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | The formatted string corresponding to the resource name. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |
  | 9001006 | The resource is referenced cyclically. |
  | 9001007 | Failed to format the resource obtained based on the resource ID. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let resource = @r(app.string.test)
    resourceManager.getString(resource.id, ArgsValueType.StringValue("format string"), ArgsValueType.Int32Value(10), ArgsValueType.Float32Value(98.78))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getStringArrayByName(String)

```cangjie
public func getStringArrayByName(resName: String): Array<String>
```

**Function:** Retrieves the string array resource corresponding to the resource name.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resName | String | Yes | - | Resource name. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | The string array resource corresponding to the resource name. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001003 | Invalid resource name. |
  | 9001004 | No matching resource is found based on the resource name. |
  | 9001006 | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    resourceManager.getStringArrayByName("test")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getStringArrayValue(UInt32)

```cangjie
public func getStringArrayValue(resId: UInt32): Array<String>
```

**Function:** Retrieves the string array resource corresponding to the resource ID.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resId | UInt32 | Yes | - | Resource ID. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | The string array corresponding to the resource ID. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |
  | 9001006 | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.strarray.test)
    resourceManager.getStringArrayValue(res.id)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getStringArrayValue(AppResource)

```cangjie
public func getStringArrayValue(resource: AppResource): Array<String>
```

**Function:** Retrieves the string array resource corresponding to the resource object. This interface is used for cross-package access in multi-project applications.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resource | [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource) | Yes | - | Resource object. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | The string array corresponding to the resource object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001001 | Invalid resource ID. |
  | 9001002 | No matching resource is found based on the resource ID. |
  | 9001006 | The resource is referenced cyclically. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let res = @r(app.strarray.test)
    let resource = AppResource("com.example.myapplication", "entry", res.id)
    resourceManager.getStringArrayValue(resource)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getStringByName(String, Array\<ArgsValueType>)

```cangjie
public func getStringByName(resName: String, args: Array<ArgsValueType>): String
```

**Function:** Retrieves the string resource corresponding to the resource name and formats it based on the args parameters.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resName | String | Yes | - | Resource name. |
| args | Array\<[ArgsValueType](#enum-argsvaluetype)> | Yes | - | Parameters for formatting the string resource. <br>Supported parameter types: <br /> %d, %f, %s, %%. <br>Note: %% is an escape character that translates to %. <br>Example: %%d will be formatted as the string %d. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | The formatted string corresponding to the resource name. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001003 | Invalid resource name. |
  | 9001004 | No matching resource is found based on the resource name. |
  | 9001006 | The resource is referenced cyclically. |
  | 9001007 | Failed to format the resource obtained based on the resource ID. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    resourceManager.getStringByName("test", ArgsValueType.StringValue("format string"), ArgsValueType.Int32Value(10), ArgsValueType.Float32Value(98.78))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func removeResource(String)

```cangjie
public func removeResource(path: String): Unit
```

**Function:** Removes the specified resource path at runtime and restores the resources to their state before being overridden.

**System Capability:** SystemCapability.Global.ResourceManager

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Resource path. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Resource Management Error Codes](./cj-errorcode-resource-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 9001010 | Invalid overlay path. |

- IllegalStateException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | If the instance id is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocalizationKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let resourceManager = Global.getResourceManager()
    let path = "/data/storage/el2/base/haps/entry/files/library-default-unsigned.hsp"
    resourceManager.removeResource(path)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## enum ArgsValueType

```cangjie
public enum ArgsValueType {
    | Int32Value(Int32)
    | Float32Value(Float32)
    | StringValue(String)
    | ...
}
```

**Description:** Enumeration type for formatted string resource parameters.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### Float32Value(Float32)

```cangjie
Float32Value(Float32)
```

**Description:** Enumeration value for Float32 type formatted string resource parameters.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### Int32Value(Int32)

```cangjie
Int32Value(Int32)
```

**Description:** Enumeration value for Int32 type formatted string resource parameters.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### StringValue(String)

```cangjie
StringValue(String)
```

**Description:** Enumeration value for String type formatted string resource parameters.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

## enum ColorMode

```cangjie
public enum ColorMode {
    | Dark
    | Light
    | ...
}
```

**Description:** Represents the current device color mode.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### Dark

```cangjie
Dark
```

**Description:** Dark mode.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### Light

```cangjie
Light
```

**Description:** Light mode.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

## enum DeviceType

```cangjie
public enum DeviceType {
    | DeviceTypePhone
    | DeviceTypeTablet
    | DeviceTypeCar
    | DeviceTypePc
    | DeviceTypeTv
    | DeviceTypeWearable
    | DeviceType2In1
    | ...
}
```

**Description:** Represents the current device type.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### DeviceType2In1

```cangjie
DeviceType2In1
```

**Description:** 2-in-1 device.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### DeviceTypeCar

```cangjie
DeviceTypeCar
```

**Description:** Car.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### DeviceTypePc

```cangjie
DeviceTypePc
```

**Description:** PC.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### DeviceTypePhone

```cangjie
DeviceTypePhone
```

**Description:** Phone.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### DeviceTypeTv

```cangjie
DeviceTypeTv
```

**Description:** TV.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### DeviceTypeTablet

```cangjie
DeviceTypeTablet
```

**Description:** Tablet.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### DeviceTypeWearable

```cangjie
DeviceTypeWearable
```

**Description:** Wearable device.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

## enum Direction

```cangjie
public enum Direction {
    | DirectionVertical
    | DirectionHorizontal
    | ...
}
```

**Description:** Represents device screen orientation.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### DirectionHorizontal

```cangjie
DirectionHorizontal
```

**Description:** Landscape orientation.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### DirectionVertical

```cangjie
DirectionVertical
```

**Description:** Portrait orientation.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

## enum NumberValueType

```cangjie
public enum NumberValueType {
    | Int32Value(Int32)
    | Float32Value(Float32)
    | ...
}
```

**Description:** Represents numeric types obtained from resources.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### Float32Value(Float32)

```cangjie
Float32Value(Float32)
```

**Description:** Number type storing Float32 values.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### Int32Value(Int32)

```cangjie
Int32Value(Int32)
```

**Description:** Number type storing Int32 values.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

## enum ScreenDensity

```cangjie
public enum ScreenDensity {
    | ScreenSdpi
    | ScreenMdpi
    | ScreenLdpi
    | ScreenXldpi
    | ScreenXxldpi
    | ScreenXxxldpi
    | ...
}
```

**Description:** Represents current device screen density.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### ScreenLdpi

```cangjie
ScreenLdpi
```

**Description:** Large-scale screen density.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### ScreenMdpi

```cangjie
ScreenMdpi
```

**Description:** Medium-scale screen density.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### ScreenSdpi

```cangjie
ScreenSdpi
```

**Description:** Small-scale screen density.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### ScreenXldpi

```cangjie
ScreenXldpi
```

**Description:** Extra large-scale screen density.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### ScreenXxldpi

```cangjie
ScreenXxldpi
```

**Description:** Extra extra large-scale screen density.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22

### ScreenXxxldpi

```cangjie
ScreenXxxldpi
```

**Description:** Extra extra extra large-scale screen density.

**System Capability:** SystemCapability.Global.ResourceManager

**Since:** 22