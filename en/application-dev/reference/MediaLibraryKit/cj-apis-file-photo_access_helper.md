# ohos.file.photo_access_helper

This module provides capabilities for album management, including creating albums and accessing/modifying media data within albums.

## Import Module

```cangjie
import kit.MediaLibraryKit.*
```

## Permission List

ohos.permission.READ_IMAGEVIDEO

ohos.permission.WRITE_IMAGEVIDEO

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example projects and configuration templates mentioned above, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## func getPhotoAccessHelper(UIAbilityContext)

```cangjie
public func getPhotoAccessHelper(context: UIAbilityContext): PhotoAccessHelper
```

**Description:** Obtains an instance of the album management module for accessing and modifying media files in albums.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|Yes|-|The Context of the Ability instance.|

**Return Value:**

|Type|Description|
|:----|:----|
|[PhotoAccessHelper](./cj-apis-file-photo_access_helper.md#class-photoaccesshelper)|Instance of the album management module.|

**Exceptions:**

- BusinessException: Error codes as shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*

let ctx = Global.getAbilityContext() // Application context needs to be obtained. See usage instructions above.
let phAccessHelper = getPhotoAccessHelper(ctx)
```

## class AbsAlbum

```cangjie
public open class AbsAlbum {}
```

**Description:** The AbsAlbum module.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### prop albumName

```cangjie
public mut prop albumName: String
```

**Description:** Album name. Preset albums are read-only, while user-created albums are writable.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### prop albumSubtype

```cangjie
public prop albumSubtype: AlbumSubtype
```

**Description:** Album subtype.

**Type:** [AlbumSubtype](./cj-apis-file-photo_access_helper.md#enum-albumsubtype)

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### prop albumType

```cangjie
public prop albumType: AlbumType
```

**Description:** Album type.

**Type:** [AlbumType](./cj-apis-file-photo_access_helper.md#enum-albumtype)

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### prop albumUri

```cangjie
public prop albumUri: String
```

**Description:** Album URI.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### prop count

```cangjie
public prop count: Int32
```

**Description:** Number of files in the album.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### prop coverUri

```cangjie
public prop coverUri: String
```

**Description:** Cover file URI.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### func getAssets(FetchOptions)

```cangjie
public func getAssets(options: FetchOptions): PhotoAssetResult
```

**Description:** Retrieves files from the album.

**Required Permission:** ohos.READ_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|options|[FetchOptions](./cj-apis-file-photo_access_helper.md#class-fetchoptions)|Yes|-| Retrieval options.|

**Return Value:**

|Type|Description|
|:----|:----|
|[PhotoAssetResult](#class-photoassetresult)|Returns a result set of image and video data.|

**Exceptions:**

- BusinessException: Error codes as shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### init(Int64)

```cangjie
public protected init(id: Int64)
```

**Description:** Constructs an AbsAlbum object.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|id|Int64|Yes|-|The ID of the AbsAlbum object to be constructed.|

## class Album

```cangjie
public class Album <: AbsAlbum {}
```

**Description:** Physical album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parent Type:**

- [AbsAlbum](#class-absalbum)

### prop imageCount

```cangjie
public prop imageCount: Int32
```

**Description:** Gets the number of images in the album.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### prop videoCount

```cangjie
public prop videoCount: Int32
```

**Description:** Gets the number of videos in the album.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### func commitModify()

```cangjie
public func commitModify(): Unit
```

**Description:** Commits album property modifications to the database.

**Required Permission:** ohos.WRITE_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Exceptions:**

- BusinessException: Error codes as shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.getAbilityContext() // Application context needs to be obtained. See usage instructions above.
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
predicates.equalTo('album_name', Str('test1'))
let fetchOptions: FetchOptions = FetchOptions(fetchColumns: [], predicates: predicates)
let fetchResult: FetchResult<Album> = phAccessHelper.getAlbums(AlbumType.USER,
    AlbumSubtype.USER_GENERIC, options: fetchOptions)
let firstAlbum = fetchResult.getFirstObject()
firstAlbum.albumName = "test10086"
firstAlbum.commitModify()
```  

## class AlbumResult

```cangjie
public class AlbumResult <: FetchResult {}
```

**Description:** Album result module.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parent Type:**

- [FetchResult](#class-fetchresult)

### func getAllObjects()

```cangjie
public func getAllObjects(): Array<Album>
```

**Description:** Retrieves all assets in the album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|Array\<[Album](#class-album)>|Returns a list of albums.|

**Exceptions:**

- BusinessException: Error codes as shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getFirstObject()

```cangjie
public func getFirstObject(): Album
```

**Description:** Retrieves the first file asset in the album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|[Album](#class-album)|Returns the first album.|

**Exceptions:**

- BusinessException: Error codes as shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getLastObject()

```cangjie
public func getLastObject(): Album
```

**Description:** Retrieves the last file asset in the album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|[Album](#class-album)|Returns the last album.|

**Exceptions:**

- BusinessException: Error codes as shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getNextObject()

```cangjie
public func getNextObject(): Album
```

**Description:** Retrieves the next file asset in the album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|[Album](#class-album)|Returns the next album.|

**Exceptions:**

- BusinessException: Error codes as shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getObjectByPosition(Int32)

```cangjie
public func getObjectByPosition(index: Int32): Album
```

**Description:** Retrieves the file asset at the specified index in the file retrieval result.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|index|Int32|Yes|-|The index of the file to retrieve, starting from 0.|

**Return Value:**

|Type|Description|
|:----|:----|
|[Album](#class-album)|The retrieved file asset.|

**Exceptions:**

- BusinessException: Error codes as shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |## class FetchResult

```cangjie
public open class FetchResult {}
```

**Description:** File retrieval result set.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### func close()

```cangjie
public func close(): Unit
```

**Description:** Releases the FetchResult instance and invalidates it. No other methods can be called afterward.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // Context application context needs to be obtained. Refer to the usage instructions in this document.
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult: PhotoAccessResult = phAccessHelper.getAssets(fetchOptions)
fetchResult.close()
```

### func getCount()

```cangjie
public func getCount(): Int32
```

**Description:** Gets the total number of files in the file retrieval result.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Int32 | Total number of retrieved files. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // Context application context needs to be obtained. Refer to the usage instructions in this document.
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult: PhotoAccessResult = phAccessHelper.getAssets(fetchOptions)
let count = fetchResult.getCount()
```

### func isAfterLast()

```cangjie
public func isAfterLast(): Bool
```

**Description:** Checks if the result set points to the last row.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns true if there are no records after reading the last one; otherwise, returns false. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // Context application context needs to be obtained. Refer to the usage instructions in this document.
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult: PhotoAccessResult = phAccessHelper.getAssets(fetchOptions)
let isAfterLast = fetchResult.isAfterLast()
```

### init(Int64)

```cangjie
public protected init(id: Int64)
```

**Description:** Constructs a FetchResult object.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| id | Int64 | Yes | - | ID of the FetchResult object to be constructed. |

## class PhotoAsset

```cangjie
public class PhotoAsset {}
```

**Description:** Provides methods to encapsulate file attributes.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### prop displayName

```cangjie
public prop displayName: String
```

**Description:** Gets the file name, including the extension.

**Type:** String

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### prop photoType

```cangjie
public prop photoType: PhotoType
```

**Description:** Gets the media file type.

**Type:** [PhotoType](#enum-phototype)

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### prop uri

```cangjie
public prop uri: String
```

**Description:** Gets the media file resource URI.

**Type:** String

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### func commitModify()

```cangjie
public func commitModify(): Unit
```

**Description:** Modifies the file's metadata.

**Required Permission:** ohos.permission.WRITE_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000001 | Invalid display name |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.*

let ctx = Global.getAbilityContext() // Context application context needs to be obtained. Refer to the usage instructions in this document.
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchColumns = [PhotoKeys
    .TITLE
    .toString()]
let fetchOptions: FetchOptions = FetchOptions(fetchColumns: fetchColumns, predicates: predicates
)
let fetchResult: FetchResult<PhotoAsset> = phAccessHelper.getAssets(fetchOptions)
let firstPhotoAsset = fetchResult.getFirstObject()
let photoAssetTitle = firstPhotoAsset
    .get('title')
    .getString()
let newTitle = "123456789"
firstPhotoAsset.set('title', newTitle)
firstPhotoAsset.commitModify()
```

### func get(String)

```cangjie
public func get(member: String): MemberType
```

**Description:** Gets the member parameter of PhotoAsset.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| member | String | Yes | - | Member parameter name. When getting, except for 'uri', 'media_type', 'subtype', and 'display_name', other attributes need to specify the [PhotoKeys](./cj-apis-file-photo_access_helper.md#enum-photokeys) to be retrieved in fetchColumns. For example, to get the title attribute: fetchColumns: ['title']. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [MemberType](#enum-membertype) | Value of the PhotoAsset member parameter. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 13900020 | Invalid argument |
  | 14000014 | The provided member must be a property name of PhotoKey. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.*

let ctx = Global.getAbilityContext() // Context application context needs to be obtained. Refer to the usage instructions in this document.
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchColumns = [PhotoKeys
    .TITLE
    .toString()]
let fetchOptions: FetchOptions = FetchOptions(fetchColumns: fetchColumns, predicates: predicates
)
let fetchResult: FetchResult<PhotoAsset> = phAccessHelper.getAssets(fetchOptions)
let firstPhotoAsset = fetchResult.getFirstObject()
let photoAssetTitle = firstPhotoAsset
    .get('title')
    .getString()
```

### func getThumbnail(?Size)

```cangjie
public func getThumbnail(size!: ?Size = Size(256, 256)): PixelMap
```

**Description:** Gets the thumbnail of the file with the specified size.

**Required Permission:** ohos.permission.WRITE_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| size | ?[Size](../ImageKit/cj-apis-image.md#class-size) | No | Size(256, 256) | **Named parameter.** Thumbnail size. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap) | Returns the PixelMap of the thumbnail. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 13900012 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.*

let ctx = Global.getAbilityContext() // Context application context needs to be obtained. Refer to the usage instructions in this document.
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchColumns = [PhotoKeys
    .TITLE
    .toString()]
let fetchOptions: FetchOptions = FetchOptions(fetchColumns: fetchColumns, predicates: predicates
)
let fetchResult: FetchResult<PhotoAsset> = phAccessHelper.getAssets(fetchOptions)
let firstPhotoAsset = fetchResult.getFirstObject()
let pixm = firstPhotoAsset.getThumbnail()
```

### func set(String, String)

```cangjie
public func set(member: String, value: String): Unit
```

**Description:** Sets the member parameter of PhotoAsset.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| member | String | Yes | - | Member parameter name, e.g., [PhotoKeys](./cj-apis-file-photo_access_helper.md#enum-photokeys).TITLE. |
| value | String | Yes | - | Sets the member parameter name. Only the value of [PhotoKeys](./cj-apis-file-photo_access_helper.md#enum-photokeys).TITLE can be modified. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 13900020 | Invalid argument |
  | 14000014 | The provided member must be a property name of PhotoKey. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.*

let ctx = Global.getAbilityContext() // Context application context needs to be obtained. Refer to the usage instructions in this document.
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchColumns = [PhotoKeys
    .TITLE
    .toString()]
let fetchOptions: FetchOptions = FetchOptions(fetchColumns: fetchColumns, predicates: predicates
)
let fetchResult: FetchResult<PhotoAsset> = phAccessHelper.getAssets(fetchOptions)
let firstPhotoAsset = fetchResult.getFirstObject()
let photoAssetTitle = firstPhotoAsset
    .get('title')
    .getString()
let newTitle = "123456789"
firstPhotoAsset.set('title', newTitle)
```## class PhotoAssetResult

```cangjie
public class PhotoAssetResult <: FetchResult {}
```

**Function:** Provides methods for encapsulating file attributes.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parent Type:**

- [FetchResult](#class-fetchresult)

### func getAllObjects()

```cangjie
public func getAllObjects(): Array<PhotoAsset>
```

**Function:** Retrieves all file assets in the file query result set.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<[PhotoAsset](#class-photoasset)> | Returns an array of all file assets in the result set. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getFirstObject()

```cangjie
public func getFirstObject(): PhotoAsset
```

**Function:** Retrieves the first file asset in the file query result set.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| [PhotoAsset](#class-photoasset) | Returns the first object in the result set. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getLastObject()

```cangjie
public func getLastObject(): PhotoAsset
```

**Function:** Retrieves the last file asset in the file query result set.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| [PhotoAsset](#class-photoasset) | Returns the last object in the result set. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getNextObject()

```cangjie
public func getNextObject(): PhotoAsset
```

**Function:** Retrieves the next file asset in the file query result set.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| [PhotoAsset](#class-photoasset) | Returns the next object in the result set. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getObjectByPosition(Int32)

```cangjie
public func getObjectByPosition(index: Int32): PhotoAsset
```

**Function:** Retrieves the file asset at the specified index in the file query result set.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| index | Int32 | Yes | - | The index of the file to retrieve, starting from 0. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [PhotoAsset](#class-photoasset) | The retrieved file asset. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

## enum MemberType

```cangjie
public enum MemberType {
    | Int64Value(Int64)
    | StringValue(String)
    | BoolValue(Bool)
    | ...
}
```

**Function:** Member types of PhotoAsset.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### Int64Value

```cangjie
Int64Value(Int64)
```

**Function:** Int64 type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### StringValue

```cangjie
StringValue(String)
```

**Function:** String type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### BoolValue

```cangjie
BoolValue(Bool)
```

**Function:** Bool type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

## enum PhotoType

```cangjie
public enum PhotoType <: Equatable<PhotoType> & ToString {
    | Image
    | Video
    | ...
}
```

**Function:** Media file types.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

**Parent Types:**

- Equatable\<PhotoType>
- ToString

### Image

```cangjie
Image
```

**Function:** Image.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### Video

```cangjie
Video
```

**Function:** Video.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 21

### func !=(PhotoType)

```cangjie
public operator func !=(other: PhotoType): Bool
```

**Function:** Determines whether two enum values are not equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [PhotoType](#enum-phototype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns true if the two enum values are not equal, otherwise returns false. |

### func ==(PhotoType)

```cangjie
public operator func ==(other: PhotoType): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [PhotoType](#enum-phototype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns true if the two enum values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Retrieves the value of the enum.

**Return Value:**

| Type | Description |
| :---- | :---- |
| String | The description of the enum. |