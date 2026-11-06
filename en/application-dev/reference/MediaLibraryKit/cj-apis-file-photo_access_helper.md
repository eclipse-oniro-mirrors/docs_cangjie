# ohos.file.photo_access_helper

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module provides capabilities for album management, including creating albums and accessing/modifying media data within albums.

## Importing the Module

```cangjie
import kit.MediaLibraryKit.*
```

## Permission List

ohos.permission.READ_IMAGEVIDEO

ohos.permission.WRITE_IMAGEVIDEO

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-sample-code-instructions).

## func getPhotoAccessHelper(UIAbilityContext)

```cangjie
public func getPhotoAccessHelper(context: UIAbilityContext): PhotoAccessHelper
```

**Function:** Obtains an instance of the album management module for accessing and modifying media files in albums.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The Context of the Ability instance. |

**Return Value:**

| Type | Description |
|:----|:----|
| [PhotoAccessHelper](./cj-apis-file-photo_access_helper.md#class-photoaccesshelper) | An instance of the album management module. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // The Context application context needs to be obtained. See the usage instructions above.
    let phAccessHelper = getPhotoAccessHelper(ctx)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface MediaChangeRequest

```cangjie
public interface MediaChangeRequest {}
```

**Function:** Media change request, the parent type for asset change requests and album change requests.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

## class AbsAlbum

```cangjie
public open class AbsAlbum {}
```

**Function:** The AbsAlbum module.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### prop albumName

```cangjie
public mut prop albumName: String
```

**Function:** The name of the album. Preset albums are read-only, while user-created albums are writable.

**Type:** String

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### prop albumSubtype

```cangjie
public prop albumSubtype: AlbumSubtype
```

**Function:** The subtype of the album.

**Type:** [AlbumSubtype](#enum-albumsubtype)

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### prop albumType

```cangjie
public prop albumType: AlbumType
```

**Function:** The type of the album.

**Type:** [AlbumType](#enum-albumtype)

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### prop albumUri

```cangjie
public prop albumUri: String
```

**Function:** The URI of the album.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### prop count

```cangjie
public prop count: Int32
```

**Function:** The number of files in the album.

**Type:** Int32

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### prop coverUri

```cangjie
public prop coverUri: String
```

**Function:** The URI of the cover file.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func getAssets(FetchOptions)

```cangjie
public func getAssets(options: FetchOptions): PhotoAssetResult
```

**Function:** Retrieves files from the album.

**Required Permission:** ohos.permission.READ_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| options | [FetchOptions](./cj-apis-file-photo_access_helper.md#class-fetchoptions) | Yes | - | The retrieval options. |

**Return Value:**

| Type | Description |
|:----|:----|
| [PhotoAssetResult](#class-photoassetresult) | Returns a result set of image and video data. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

## class Album

```cangjie
public class Album <: AbsAlbum {}
```

**Function:** A physical album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Type:**

- [AbsAlbum](#class-absalbum)

### prop imageCount

```cangjie
public prop imageCount: Int32
```

**Function:** Gets the number of images in the album.

**Type:** Int32

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### prop videoCount

```cangjie
public prop videoCount: Int32
```

**Function:** Gets the number of videos in the album.

**Type:** Int32

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func commitModify()

```cangjie
public func commitModify(): Unit
```

**Function:** Commits album property modifications to the database.

**Required Permission:** ohos.permission.WRITE_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // The Context application context needs to be obtained. See the usage instructions above.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    predicates.equalTo('album_name', StringValue('test1'))
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAlbums(AlbumType.User,
        AlbumSubtype.UserGeneric, options: fetchOptions)
    let firstAlbum = fetchResult.getFirstObject()
    firstAlbum.albumName = "test10086"
    firstAlbum.commitModify()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```  

## class AlbumResult

```cangjie
public class AlbumResult <: FetchResult {}
```

**Function:** The album result module.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Type:**

- [FetchResult](#class-fetchresult)

### func getAllObjects()

```cangjie
public func getAllObjects(): Array<Album>
```

**Function:** Gets all assets in the album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[Album](#class-album)> | Returns a list of albums. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // The Context application context needs to be obtained. See the usage instructions above.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    predicates.equalTo('album_name', StringValue('test1'))
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAlbums(AlbumType.User,
        AlbumSubtype.UserGeneric, options: fetchOptions)
    let albums = fetchResult.getAllObjects()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```  

### func getFirstObject()

```cangjie
public func getFirstObject(): Album
```

**Function:** Gets the first file asset in the album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Album](#class-album) | Returns the first album. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // The Context application context needs to be obtained. See the usage instructions above.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    predicates.equalTo('album_name', StringValue('test1'))
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAlbums(AlbumType.User,
        AlbumSubtype.UserGeneric, options: fetchOptions)
    let album = fetchResult.getFirstObject()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```  

### func getLastObject()

```cangjie
public func getLastObject(): Album
```

**Function:** Gets the last file asset in the album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Album](#class-album) | Returns the last album. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // The Context application context needs to be obtained. See the usage instructions above.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    predicates.equalTo('album_name', StringValue('test1'))
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAlbums(AlbumType.User,
        AlbumSubtype.UserGeneric, options: fetchOptions)
    let album = fetchResult.getLastObject()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```  

### func getNextObject()

```cangjie
public func getNextObject(): Album
```

**Function:** Gets the next file asset in the album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Album](#class-album) | Returns the next album. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // The Context application context needs to be obtained. See the usage instructions above.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    predicates.equalTo('album_name', StringValue('test1'))
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAlbums(AlbumType.User,
        AlbumSubtype.UserGeneric, options: fetchOptions)
    let album = fetchResult.getNextObject()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
``` 

### func getObjectByPosition(Int32)

```cangjie
public func getObjectByPosition(index: Int32): Album
```

**Function:** Gets the file asset at the specified index in the file retrieval result.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| index | Int32 | Yes | - | The index of the file to retrieve, starting from 0. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Album](#class-album) | The retrieved file asset. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // The Context application context needs to be obtained. See the usage instructions above.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    predicates.equalTo('album_name', StringValue('test1'))
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAlbums(AlbumType.User,
        AlbumSubtype.UserGeneric, options: fetchOptions)
    let album = fetchResult.getObjectByPosition(0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class ChangeData

```cangjie
public class ChangeData {
    public var notifyType: NotifyType
    public var uris: Array<String>
    public var extraUris: Array<String>
}
```

**Function:** Value of the listener callback function.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var extraUris

```cangjie
public var extraUris: Array<String>
```

**Function:** Array of URIs for changed files in the album.

**Type:** Array\<String>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var notifyType

```cangjie
public var notifyType: NotifyType
```

**Function:** Notification type of ChangeData.

**Type:** [NotifyType](#enum-notifytype)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var uris

```cangjie
public var uris: Array<String>
```

**Function:** All URIs with the same [NotifyType](#enum-notifytype), which can be PhotoAsset or Album.

**Type:** Array\<String>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

## class CreateOptions

```cangjie
public class CreateOptions {
    public var title: String = ""
    public var subtype: PhotoSubtype
    public init(title!: String = "", subtype!: PhotoSubtype = Default)
}
```

**Function:** Creation options for images or videos.

Specifications for the title parameter:

- Should not include file extensions.
- String length should be between 1 and 255 characters.
- Illegal English characters are not allowed, including: . .. \ / : * ? " ' ` < > | { } [ ]

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var subtype

```cangjie
public var subtype: PhotoSubtype
```

**Function:** Title of the image or video.

**Type:** [PhotoSubtype](#enum-photosubtype)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var title

```cangjie
public var title: String = ""
```

**Function:** Title of the image or video.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### init(String, PhotoSubtype)

```cangjie
public init(title!: String = "", subtype!: PhotoSubtype = Default)
```

**Function:** Constructs a CreateOptions object.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| title | String | No | "" | **Named parameter.** Title of the image or video. |
| subtype | [PhotoSubtype](#enum-photosubtype) | No | Default | **Named parameter.** Subtype of the image or video file. |

## class FetchOptions

```cangjie
public class FetchOptions {
    public var fetchColumns: Array<String>
    public var predicates: DataSharePredicates
    public init(fetchColumns: Array<String>, predicates: DataSharePredicates)
}
```

**Function:** Retrieval conditions.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var fetchColumns

```cangjie
public var fetchColumns: Array<String>
```

**Function:** Retrieval conditions.

**Type:** Array\<String>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var predicates

```cangjie
public var predicates: DataSharePredicates
```

**Function:** Predicate query.

**Type:** [DataSharePredicates](../ArkData/cj-apis-data_share_predicates.md#class-datasharepredicates)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### init(Array\<String>, DataSharePredicates)

```cangjie
public init(fetchColumns: Array<String>, predicates: DataSharePredicates)
```

**Function:** Constructs a FetchOptions object.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fetchColumns | Array\<String> | Yes | - | Retrieval conditions, specifying column names for query. <br>For photos, if this parameter is empty, it defaults to querying 'uri', 'media_type', 'subtype', and 'display_name'. Example: fetchColumns: ['uri', 'title']. <br>For albums, if this parameter is empty, it defaults to querying 'uri' and 'album_name'. |
| predicates | [DataSharePredicates](../ArkData/cj-apis-data_share_predicates.md#class-datasharepredicates) | Yes | - | Predicate query, displaying filtering conditions. |

## class FetchResult

```cangjie
public open class FetchResult {}
```

**Function:** File retrieval result set.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func close()

```cangjie
public func close(): Unit
```

**Function:** Releases the FetchResult instance and invalidates it. No other methods can be called.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    fetchResult.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getCount()

```cangjie
public func getCount(): Int32
```

**Function:** Gets the total number of files in the file retrieval result.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Total number of files retrieved. |

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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    let count = fetchResult.getCount()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isAfterLast()

```cangjie
public func isAfterLast(): Bool
```

**Function:** Checks if the result set points to the last row.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true when reading the last record and no subsequent records exist; otherwise, returns false. |

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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    let isAfterLast = fetchResult.isAfterLast()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class MediaAlbumChangeRequest

```cangjie
public class MediaAlbumChangeRequest <: MediaChangeRequest {
    public init(album: Album)
}
```

**Function:** Album change request.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Type:**

- [MediaChangeRequest](#interface-mediachangerequest)

### init(Album)

```cangjie
public init(album: Album)
```

**Function:** Constructs a MediaAlbumChangeRequest object.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| album | [Album](./cj-apis-file-photo_access_helper.md#class-album) | Yes | - | Album to be modified. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAlbums(AlbumType.User, AlbumSubtype.UserGeneric,
        options: fetchOptions)
    let album = fetchResult.getFirstObject()
    let albumChangeRequest = MediaAlbumChangeRequest(album)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func addAssets(Array\<PhotoAsset>)

```cangjie
public func addAssets(assets: Array<PhotoAsset>): Unit
```

**Function:** Adds assets to the album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| assets | Array\<[PhotoAsset](./cj-apis-file-photo_access_helper.md#class-photoasset)> | Yes | - | Array of assets to be added to the album. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    let asset = fetchResult.getFirstObject()
    let albumFetchResult = phAccessHelper.getAlbums(AlbumType.User, AlbumSubtype.UserGeneric)
    let album = albumFetchResult.getFirstObject()
    let albumChangeRequest = MediaAlbumChangeRequest(album)
    albumChangeRequest.addAssets([asset, asset])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getAlbum()

```cangjie
public func getAlbum(): Album
```

**Function:** Gets the album in the current album change request.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Album](./cj-apis-file-photo_access_helper.md#class-album) | Returns the album in the current album change request. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAlbums(AlbumType.User, AlbumSubtype.UserGeneric,
        options: fetchOptions)
    let album = fetchResult.getFirstObject()
    let albumChangeRequest = MediaAlbumChangeRequest(album)
    var changeRequestAlbum = albumChangeRequest.getAlbum()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func removeAssets(Array\<PhotoAsset>)

```cangjie
public func removeAssets(assets: Array<PhotoAsset>): Unit
```

**Function:** Removes assets from the album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| assets | Array\<[PhotoAsset](./cj-apis-file-photo_access_helper.md#class-photoasset)> | Yes | - | Array of assets to be removed from the album. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let albumFetchResult = phAccessHelper.getAlbums(AlbumType.User, AlbumSubtype.UserGeneric)
    let album = albumFetchResult.getFirstObject()
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    let asset = fetchResult.getFirstObject()
    let albumChangeRequest = MediaAlbumChangeRequest(album)
    albumChangeRequest.removeAssets([asset])
    phAccessHelper.applyChanges(albumChangeRequest)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setAlbumName(String)

```cangjie
public func setAlbumName(name: String): Unit
```

**Function:** Sets the album name.

Specifications for the album name parameter:

- Album name string length should be between 1 and 255 characters.
- Illegal characters are not allowed, including: . .. \ / : * ? " ' ` < > | { } [ ]
- English characters are case-insensitive.
- Duplicate album names are not allowed.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Album name to be set. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try## class MediaAssetChangeRequest

```cangjie
public class MediaAssetChangeRequest <: & MediaChangeRequest {
    public init(asset: PhotoAsset)
}
```

**Function:** Asset change request.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Type:**

- [MediaChangeRequest](#interface-mediachangerequest)

### init(PhotoAsset)

```cangjie
public init(asset: PhotoAsset)
```

**Function:** Constructs a MediaAssetChangeRequest object.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| asset | [PhotoAsset](./cj-apis-file-photo_access_helper.md#class-photoasset) | Yes | - | The asset to be modified. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    let photoAsset = fetchResult.getFirstObject()
    let assetChangeRequest = MediaAssetChangeRequest(photoAsset)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func createAssetRequest(UIAbilityContext, PhotoType, String, CreateOptions)

```cangjie
public static func createAssetRequest(context: UIAbilityContext, photoType: PhotoType, extension: String,
    options!: CreateOptions = CreateOptions(title: "", subtype: Default)): MediaAssetChangeRequest
```

**Function:** Creates an asset change request by specifying the file type and extension to be created.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The Context of the Ability instance. |
| photoType | [PhotoType](./cj-apis-file-photo_access_helper.md#enum-phototype) | Yes | - | The type of file to be created, either IMAGE or VIDEO. |
| extension | String | Yes | - | The file extension, e.g., 'jpg'. |
| options | [CreateOptions](#class-createoptions) | No | CreateOptions(title: "", subtype: Default) | **Named parameter.** Creation options, e.g., {title: 'testPhoto'}. |

**Return Value:**

| Type | Description |
|:----|:----|
| [MediaAssetChangeRequest](#class-mediaassetchangerequest) | Returns the change request for creating the asset. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let photoType = PhotoType.Image
    let extension = "jpg"
    let options = CreateOptions(title: "testPhoto")
    let assetChangeRequest = MediaAssetChangeRequest.createAssetRequest(ctx, photoType,
        extension, options: options)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func createImageAssetRequest(UIAbilityContext, String)

```cangjie
public static func createImageAssetRequest(context: UIAbilityContext, fileUri: String): MediaAssetChangeRequest
```

**Function:** Creates an image asset change request.

Specifies the data source of the asset to be created via fileUri. Refer to [FileUri](../CoreFileKit/cj-apis-file_fileuri.md).

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The Context of the Ability instance. |
| fileUri | String | Yes | - | The data source of the image asset, a URI within the application sandbox. |

**Return Value:**

| Type | Description |
|:----|:----|
| [MediaAssetChangeRequest](#class-mediaassetchangerequest) | Returns the change request for creating the asset. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | The file corresponding to the URI is not in the app sandbox. |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let fileUri = "file://com.example.xxx/data/storage/el2/base/haps/entry/files/test.jpg"
    let assetChangeRequest = MediaAssetChangeRequest.createImageAssetRequest(ctx,
        fileUri)
    phAccessHelper.applyChanges(assetChangeRequest)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func createVideoAssetRequest(UIAbilityContext, String)

```cangjie
public static func createVideoAssetRequest(context: UIAbilityContext, fileUri: String): MediaAssetChangeRequest
```

**Function:** Creates a video asset change request.

Specifies the data source of the asset to be created via fileUri. Refer to [FileUri](../CoreFileKit/cj-apis-file_fileuri.md).

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The Context of the Ability instance. |
| fileUri | String | Yes | - | The data source of the video asset, a URI within the application sandbox. |

**Return Value:**

| Type | Description |
|:----|:----|
| [MediaAssetChangeRequest](#class-mediaassetchangerequest) | Returns the change request for creating the asset. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | The file corresponding to the URI is not in the app sandbox. |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let fileUri = "file://com.example.xxx/data/storage/el2/base/haps/entry/files/test.mp4"
    let assetChangeRequest = MediaAssetChangeRequest.createVideoAssetRequest(ctx,
        fileUri)
    phAccessHelper.applyChanges(assetChangeRequest)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func deleteAssets(UIAbilityContext, Array\<PhotoAsset>)

```cangjie
public static func deleteAssets(context: UIAbilityContext, assets: Array<PhotoAsset>): Unit
```

**Function:** Deletes media files. Deleted files are moved to the recycle bin.

**Required Permission:** ohos.permission.WRITE_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The Context of the Ability instance. |
| assets | Array\<[PhotoAsset](./cj-apis-file-photo_access_helper.md#class-photoasset)> | Yes | - | The array of URIs of the media files to be deleted. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    let asset = fetchResult.getFirstObject()
    MediaAssetChangeRequest.deleteAssets(ctx, asset.uri)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func deleteAssets(UIAbilityContext, Array\<String>)

```cangjie
public static func deleteAssets(context: UIAbilityContext, assets: Array<String>): Unit
```

**Function:** Deletes media files. Deleted files are moved to the recycle bin.

**Required Permission:** ohos.permission.WRITE_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The Context of the Ability instance. |
| assets | Array\<String> | Yes | - | The array of URIs of the media files to be deleted. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied |
  | 14000002 | The uri format is incorrect or does not exist. |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    let asset = fetchResult.getFirstObject()
    MediaAssetChangeRequest.deleteAssets(ctx, asset.uri)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func addResource(ResourceType, String)

```cangjie
public func addResource(resourceType: ResourceType, fileUri: String): Unit
```

**Function:** Adds a resource via ArrayBuffer data.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| resourceType | [ResourceType](#enum-resourcetype) | Yes | - | The type of resource to be added. |
| fileUri | String | Yes | - | The data source of the resource to be added, a URI within the application sandbox. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | The file corresponding to the URI is not in the app sandbox. |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let photoType = PhotoType.Image
    let extension = "jpg"
    let assetChangeRequest = MediaAssetChangeRequest.createAssetRequest(ctx, photoType,
        extension)
    let buffer = Array<Byte>(2048, repeat: 0)
    assetChangeRequest.addResource(ResourceType.ImageResource, buffer)
    phAccessHelper.applyChanges(assetChangeRequest)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func addResource(ResourceType, Array\<Byte>)

```cangjie
public func addResource(resourceType: ResourceType, data: Array<Byte>): Unit
```

**Function:** Adds a resource via ArrayBuffer data.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resourceType | [ResourceType](#enum-resourcetype) | Yes | - | Type of the resource to be added. |
| data | Array\<Byte> | Yes | - | Data of the resource to be added. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let photoType = PhotoType.Image
    let extension = "jpg"
    let assetChangeRequest = MediaAssetChangeRequest.createAssetRequest(ctx, photoType,
        extension)
    let buffer = Array<Byte>(2048, repeat: 0)
    assetChangeRequest.addResource(ResourceType.ImageResource, buffer)
    phAccessHelper.applyChanges(assetChangeRequest)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func discardCameraPhoto()

```cangjie
public func discardCameraPhoto(): Unit
```

**Function:** Saves a photo taken by the camera.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | Internal system error |
  | 14000016 | Operation Not Support |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    let photoAsset = fetchResult.getFirstObject()
    let assetChangeRequest = MediaAssetChangeRequest(photoAsset)
    assetChangeRequest.discardCameraPhoto()
    phAccessHelper.applyChanges(assetChangeRequest)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getAsset()

```cangjie
public func getAsset(): PhotoAsset
```

**Function:** Gets the asset in the current asset change request.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [PhotoAsset](./cj-apis-file-photo_access_helper.md#class-photoasset) | Returns the asset in the current asset change request. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    let photoAsset = fetchResult.getFirstObject()
    let assetChangeRequest = MediaAssetChangeRequest(photoAsset)
    let asset = assetChangeRequest.getAsset()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getWriteCacheHandler()

```cangjie
public func getWriteCacheHandler(): Int32
```

**Function:** Gets the temporary file write handle.

**Required Permission:** ohos.permission.WRITE_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Returns the temporary file write handle. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.CoreFileKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let assetChangeRequest = MediaAssetChangeRequest.createAssetRequest(ctx,
        PhotoType.Video, "mp4")
    let fd = assetChangeRequest.getWriteCacheHandler()
    FileIo.close(fd)
    phAccessHelper.applyChanges(assetChangeRequest)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func saveCameraPhoto()

```cangjie
public func saveCameraPhoto(): Unit
```

**Function:** Saves a photo taken by the camera.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    let photoAsset = fetchResult.getFirstObject()
    let assetChangeRequest = MediaAssetChangeRequest(photoAsset)
    assetChangeRequest.saveCameraPhoto()
    phAccessHelper.applyChanges(assetChangeRequest)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setTitle(String)

```cangjie
public func setTitle(title: String): Unit
```

**Function:** Modifies the title of a media asset.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| title | String | Yes | - | Title of the asset to be modified. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult = phAccessHelper.getAssets(fetchOptions)
    let photoAsset = fetchResult.getFirstObject()
    let assetChangeRequest = MediaAssetChangeRequest(photoAsset)
    let newTitle = "NEW_TITLE" // New title, name as needed in actual use
    assetChangeRequest.setTitle(newTitle)
    phAccessHelper.applyChanges(assetChangeRequest)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class PhotoAccessHelper

```cangjie
public class PhotoAccessHelper {}
```

**Function:** Obtains image and video resources.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func applyChanges(MediaChangeRequest)

```cangjie
public func applyChanges(mediaChangeRequest: MediaChangeRequest): Unit
```

**Function:** Submits a media change request.

**Required Permission:** ohos.permission.WRITE_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| mediaChangeRequest | [MediaChangeRequest](#interface-mediachangerequest) | Yes | - | Media change request, which supports asset change requests and album change requests. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied |
  | 14000011 | System inner fail |

### func getAlbums(AlbumType, AlbumSubtype, FetchOptions)

```cangjie
public func getAlbums(albumType: AlbumType, subtype: AlbumSubtype,
    options!: FetchOptions = FetchOptions(["uri", "album_name"], DataSharePredicates())): AlbumResult
```

**Function:** Obtains albums based on the search options and album type. Ensure that the albums exist before obtaining them.

**Required Permission:** ohos.permission.READ_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| albumType | [AlbumType](#enum-albumtype) | Yes | - | Album type. |
| subtype | [AlbumSubtype](#enum-albumsubtype) | Yes | - | Album subtype. |
| options | [FetchOptions](#class-fetchoptions) | No | FetchOptions(["uri", "album_name"], DataSharePredicates()) | **Named parameter.** Search options. |

**Return Value:**

| Type | Description |
|:----|:----|
| AlbumResult | Returns the result set of the obtained albums. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context needs to be obtained. See usage instructions in this document.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult: AlbumResult = phAccessHelper.getAlbums(AlbumType.User,
        AlbumSubtype.UserGeneric, options: fetchOptions)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func getAssets(FetchOptions)

```cangjie
public func getAssets(options: FetchOptions): PhotoAssetResult
```

**Function:** Retrieve image and video assets.

**Required Permission:** ohos.permission.READ_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| options | [FetchOptions](#class-fetchoptions) | Yes | - | Image and video retrieval options. |

**Return Value:**

| Type | Description |
|:----|:----|
| PhotoAssetResult | Returns the result set of retrieved burst photos. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult: PhotoAssetResult = phAccessHelper.getAssets(fetchOptions)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getBurstAssets(String, FetchOptions)

```cangjie
public func getBurstAssets(burstKey: String, options: FetchOptions): PhotoAssetResult
```

**Function:** Retrieve burst photo assets.

**Required Permission:** ohos.permission.READ_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| burstKey | String | Yes | - | Unique identifier for a set of burst photos: uuid (can pass [PhotoKeys](#enum-photokeys)'s BURST_KEY). |
| options | [FetchOptions](#class-fetchoptions) | Yes | - | Burst photo retrieval options. |

**Return Value:**

| Type | Description |
|:----|:----|
| PhotoAssetResult | Returns the result set of retrieved burst photos. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied |
  | 14000011 | Internal system error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let burstKey = "YOUR_UUID" // Please input uuid
    let fetchResult: PhotoAssetResult = phAccessHelper.getBurstAssets(burstKey, fetchOptions)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func registerChange(String, Bool, Callback1Argument\<ChangeData>)

```cangjie
public func registerChange(uri: String, forChildUris: Bool, callback: Callback1Argument<ChangeData>): Unit
```

**Function:** Register a listener for the specified URI, returning asynchronous results via callback.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| uri | String | Yes | - | URI of PhotoAsset, Album, or value of [DefaultChangeUri](#enum-defaultchangeuri). |
| forChildUris | Bool | Yes | - | Whether to listen vaguely. When URI is an album URI, setting forChildUris to true allows listening to changes in files within the album; if false, only changes to the album itself can be listened to. When URI is a photoAsset, forChildUris being true or false makes no difference. When URI is DefaultChangeUri, forChildUris must be true; if false, the URI cannot be found, and no messages will be received. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[ChangeData](#class-changedata)> | Yes | - | Returns the [ChangeData](#class-changedata) to be listened to. Note: Multiple different callbacks can be registered for the same URI. [unRegisterChange](#func-unregisterchangestring-callback1argumentchangedata) can close all listeners for the URI or specific callback listeners. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900012 | Permission denied |
  | 13900020 | Invalid argument |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class MyCallback<T> <: Callback1Argument<T> {
        public let callabck_: (T) -> Unit
        public init(callabck: (T) -> Unit) {
            callabck_ = callabck
        }
        public open func invoke(err: ?BusinessException, arg: T): Unit {
            callabck_(arg)
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let callback1 = MyCallback<ChangeData>(
        {
            arg: ChangeData => Hilog.info(0, "AppLogCj",
                "onCallback1. ChangeData: type = ${arg.notifyType.toString()}, uris.size: ${arg.uris.size}, extraUris.size = ${arg.extraUris.size}"
            )
        })
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions(['title'], predicates)
    let fetchResult: PhotoAssetResult = phAccessHelper.getAssets(fetchOptions)
    let firstPhotoAsset = fetchResult.getFirstObject()
    phAccessHelper.registerChange(firstPhotoAsset.uri, false, callback1)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func release()

```cangjie
public func release(): Unit
```

**Function:** Release the PhotoAccessHelper instance. Call this when the methods in the PhotoAccessHelper instance are no longer needed.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions([], predicates)
    let fetchResult: PhotoAssetResult = phAccessHelper.getAssets(fetchOptions)
    fetchResult.close()
    phAccessHelper.release()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func showAssetsCreationDialog(Array\<String>, Array\<PhotoCreationConfig>, Callback1Argument\<Array\<String>>)

```cangjie
public func showAssetsCreationDialog(srcFileUris: Array<String>, photoCreationConfigs: Array<PhotoCreationConfig>,
    callback: Callback1Argument<Array<String>>): Unit
```

**Function:** Invoke the interface to display a save confirmation dialog. After user confirmation, returns a list of URIs with permanent save permissions in the callback. These URIs can be used by the application to write images/videos. If the user declines, an empty list is returned.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| srcFileUris | Array\<String> | Yes | - | URIs of image/video files to be saved to the media library.<br>**Note:** Only image and video URIs are supported. |
| photoCreationConfigs | Array\<[PhotoCreationConfig](#class-photocreationconfig)> | Yes | - | Configuration for saving images/videos to the media library, including filenames, etc. Must correspond one-to-one with srcFileUris. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<Array\<String>> | Yes | - | Callback function to retrieve the list of media library file URIs returned to the application. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14000011 | Internal system error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class MyCallback<T> <: Callback1Argument<T> {
        public let callabck_: (T) -> Unit
        public init(callabck: (T) -> Unit) {
            callabck_ = callabck
        }
        public open func invoke(err: ?BusinessException, arg: T): Unit {
            callabck_(arg)
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let callback3 = MyCallback<Array<String>>(
        {
            arg: Array<String> =>
            Hilog.info(0, "AppLogCj", "oncallback3: Array.size: ${arg.size}")
            for (str in arg) {
                Hilog.info(0, "AppLogCj", "oncallback3: uri: ${str}")
            }
        }
    )
    // Get URIs of images/videos located in the application sandbox to be saved to the media library
    // Use actual URIs in real scenarios
    let srcFileUris: Array<String> = ["file://media/Photo/37/IMG_1731463495_028/IMG_20241113_100315.jpg"]
    let photoCreationConfigs: Array<PhotoCreationConfig> = [
        PhotoCreationConfig(
            'jpg',
            PhotoType.Image,
            title: "test4",
            subtype: PhotoSubtype.Default
        )
    ]
    phAccessHelper.showAssetsCreationDialog(srcFileUris, photoCreationConfigs, callback3)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func unRegisterChange(String, ?Callback1Argument\<ChangeData>)

```cangjie
public func unRegisterChange(uri: String, callback!: ?Callback1Argument<ChangeData> = None): Unit
```

**Function:** Unregister listeners for the specified URI. Multiple callbacks can be registered for the same URI. When multiple callback listeners exist, specific registered callbacks can be unregistered; if no callback is specified, all listeners for the URI are unregistered.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| uri | String | Yes | - | URI of PhotoAsset, Album, or value of [DefaultChangeUri](#enum-defaultchangeuri). |
| callback | ?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[ChangeData](#class-changedata)> | No | None | **Named parameter.** Unregister the callback listener registered via [registerChange](#func-registerchangestring-bool-callback1argumentchangedata). If not provided, all listeners for the URI are unregistered. Note: After unregistering a specific callback, it will no longer receive notifications. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900012 | Permission denied |
  | 13900020 | Invalid argument |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    class MyCallback<T> <: Callback1Argument<T> {
        public let callabck_: (T) -> Unit
        public init(callabck: (T) -> Unit) {
            callabck_ = callabck
        }
        public open func invoke(err: ?BusinessException, arg: T): Unit {
            callabck_(arg)
        }
    }

    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let callback1 = MyCallback<ChangeData>(
        {
            arg: ChangeData => Hilog.info(0, "AppLogCj",
                "onCallback1. ChangeData: type = ${arg.notifyType.toString()}, uris.size: ${arg.uris.size}, extraUris.size = ${arg.extraUris.size}"
            )
        })

    let predicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions(['title'], predicates)
    let fetchResult: PhotoAssetResult = phAccessHelper.getAssets(fetchOptions)
    let firstPhotoAsset = fetchResult.getFirstObject()

    phAccessHelper.registerChange(firstPhotoAsset.uri, false, callback1)
    phAccessHelper.unRegisterChange(firstPhotoAsset.uri, callback: callback1)
    phAccessHelper.unRegisterChange(firstPhotoAsset.uri)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class PhotoAsset

```cangjie
public class PhotoAsset {}
```

**Function:** Provides methods to encapsulate file attributes.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### prop displayName

```cangjie
public prop displayName: String
```

**Function:** Get the filename, including the extension.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### prop photoType

```cangjie
public prop photoType: PhotoType
```

**Function:** Get the media file type.

**Type:** [PhotoType](#enum-phototype)

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### prop uri

```cangjie
public prop uri: String
```

**Function:** Get the media file resource URI.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func commitModify()

```cangjie
public func commitModify(): Unit
```

**Function:** Modify file metadata.

**Required Permission:** ohos.permission.WRITE_IMAGEVIDEO

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ctx = Global.getAbilityContext() // Context application context required. See usage instructions for details.
    let phAccessHelper = getPhotoAccessHelper(ctx)
    let predicates = DataSharePredicates()
    let fetchColumns = [PhotoKeys.Title.toString()]
    let fetchOptions: FetchOptions = FetchOptions## class PhotoAssetResult

```cangjie
public class PhotoAssetResult <: FetchResult {}
```

**Function:** Provides methods for encapsulating file attributes.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Type:**

- [FetchResult](#class-fetchresult)

### func getAllObjects()

```cangjie
public func getAllObjects(): Array<PhotoAsset>
```

**Function:** Retrieves all file assets in the file query result set.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
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

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
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

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
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

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
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

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| index | Int32 | Yes | - | The index of the file to retrieve, starting from 0. |

**Return Value:**

| Type | Description |
|:----|:----|
| [PhotoAsset](#class-photoasset) | The retrieved file asset. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](../CoreFileKit/cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

## class PhotoCreationConfig

```cangjie
public class PhotoCreationConfig {
    public var fileNameExtension: String
    public var photoType: PhotoType
    public var title: String
    public var subtype: PhotoSubtype
    public init(fileNameExtension: String, photoType: PhotoType, title!: String = "", subtype!: PhotoSubtype = Default)
}
```

**Function:** Configuration for saving images/videos to the media library, including file names, etc.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var fileNameExtension

```cangjie
public var fileNameExtension: String
```

**Function:** File extension.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var photoType

```cangjie
public var photoType: PhotoType
```

**Function:** File type.

**Type:** [PhotoType](#enum-phototype)

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var subtype

```cangjie
public var subtype: PhotoSubtype
```

**Function:** File subtype.

**Type:** [PhotoSubtype](#enum-photosubtype)

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var title

```cangjie
public var title: String
```

**Function:** Title of the image or video.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### init(String, PhotoType, String, PhotoSubtype)

```cangjie
public init(fileNameExtension: String, photoType: PhotoType, title!: String = "", subtype!: PhotoSubtype = Default)
```

**Function:** Constructs a PhotoCreationConfig object.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fileNameExtension | String | Yes | - | File extension, e.g., 'jpg'. |
| photoType | [PhotoType](./cj-apis-file-photo_access_helper.md#enum-phototype) | Yes | - | Type of file to create: IMAGE or VIDEO. |
| title | String | No | "" | **Named parameter.** Title of the image or video. |
| subtype | [PhotoSubtype](#enum-photosubtype) | No | Default | **Named parameter.** Subtype of the image or video: Default or MovingPhoto. |

## class RequestOptions

```cangjie
public class RequestOptions {
    public var deliveryMode: DeliveryMode
}
```

**Function:** Request strategy.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### var deliveryMode

```cangjie
public var deliveryMode: DeliveryMode
```

**Function:** Resource delivery mode for requests.

**Type:** [DeliveryMode](#enum-deliverymode)

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

## enum AlbumKeys

```cangjie
public enum AlbumKeys <: ToString & Equatable<AlbumKeys> {
    | Uri
    | AlbumName
    | ...
}
```

**Function:** Key information about albums.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- ToString
- Equatable\<AlbumKeys>

### AlbumName

```cangjie
AlbumName
```

**Function:** Album name.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Uri

```cangjie
Uri
```

**Function:** Album URI.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(AlbumKeys)

```cangjie
public operator func !=(other: AlbumKeys): Bool
```

**Function:** Determines whether two enum values are not equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [AlbumKeys](#enum-albumkeys) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are not equal; otherwise, returns false. |

### func ==(AlbumKeys)

```cangjie
public operator func ==(other: AlbumKeys): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [AlbumKeys](#enum-albumkeys) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal; otherwise, returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Retrieves the value of the enum.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enum. |

## enum AlbumSubtype

```cangjie
public enum AlbumSubtype <: Equatable<AlbumSubtype> & ToString {
    | UserGeneric
    | Favorite
    | Video
    | Image
    | AnyAlbum
    | ...
}
```

**Function:** Album subtype, indicating specific album types.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- Equatable\<AlbumSubtype>
- ToString

### AnyAlbum

```cangjie
AnyAlbum
```

**Function:** Any album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Favorite

```cangjie
Favorite
```

**Function:** Favorites album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Image

```cangjie
Image
```

**Function:** Image album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### UserGeneric

```cangjie
UserGeneric
```

**Function:** User album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Video

```cangjie
Video
```

**Function:** Video album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(AlbumSubtype)

```cangjie
public operator func !=(other: AlbumSubtype): Bool
```

**Function:** Determines whether two enum values are not equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [AlbumSubtype](#enum-albumsubtype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are not equal; otherwise, returns false. |

### func ==(AlbumSubtype)

```cangjie
public operator func ==(other: AlbumSubtype): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [AlbumSubtype](#enum-albumsubtype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal; otherwise, returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Retrieves the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enum. |## enum AlbumType

```cangjie
public enum AlbumType <: Equatable<AlbumType> & ToString {
    | User
    | System
    | ...
}
```

**Description:** Album type, indicating whether it's a user album or a system preset album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- Equatable\<AlbumType>
- ToString

### System

```cangjie
System
```

**Description:** System preset album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### User

```cangjie
User
```

**Description:** User album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(AlbumType)

```cangjie
public operator func !=(other: AlbumType): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[AlbumType](#enum-albumtype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(AlbumType)

```cangjie
public operator func ==(other: AlbumType): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[AlbumType](#enum-albumtype)|Yes|-|Another enum value.|

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

## enum DefaultChangeUri

```cangjie
public enum DefaultChangeUri <: ToString & Equatable<DefaultChangeUri> {
    | DefaultPhotoUri
    | DefaultAlbumUri
    | ...
}
```

**Description:** Subtype of DefaultChangeUri.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- ToString
- Equatable\<DefaultChangeUri>

### DefaultAlbumUri

```cangjie
DefaultAlbumUri
```

**Description:** URI of the default album. When used with forSubUri{true}, it will receive change notifications for all albums.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### DefaultPhotoUri

```cangjie
DefaultPhotoUri
```

**Description:** URI of the default PhotoAsset. When used with forSubUri{true}, it will receive change notifications for all PhotoAssets.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(DefaultChangeUri)

```cangjie
public operator func !=(other: DefaultChangeUri): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[DefaultChangeUri](#enum-defaultchangeuri)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(DefaultChangeUri)

```cangjie
public operator func ==(other: DefaultChangeUri): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[DefaultChangeUri](#enum-defaultchangeuri)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|Description of the enum.|

## enum DeliveryMode

```cangjie
public enum DeliveryMode <: Equatable<DeliveryMode> & ToString {
    | FastMode
    | HighQualityMode
    | BalanceMode
    | ...
}
```

**Description:** Resource delivery mode.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- Equatable\<DeliveryMode>
- ToString

### BalanceMode

```cangjie
BalanceMode
```

**Description:** Balanced mode.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### FastMode

```cangjie
FastMode
```

**Description:** Fast mode.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### HighQualityMode

```cangjie
HighQualityMode
```

**Description:** High-quality mode.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(DeliveryMode)

```cangjie
public operator func !=(other: DeliveryMode): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[DeliveryMode](#enum-deliverymode)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(DeliveryMode)

```cangjie
public operator func ==(other: DeliveryMode): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[DeliveryMode](#enum-deliverymode)|Yes|-|Another enum value.|

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

## enum DynamicRangeType

```cangjie
public enum DynamicRangeType <: Equatable<DynamicRangeType> & ToString {
    | Sdr
    | Hdr
    | ...
}
```

**Description:** Dynamic range type of media files.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- Equatable\<DynamicRangeType>
- ToString

### Hdr

```cangjie
Hdr
```

**Description:** High dynamic range type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Sdr

```cangjie
Sdr
```

**Description:** Standard dynamic range type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(DynamicRangeType)

```cangjie
public operator func !=(other: DynamicRangeType): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[DynamicRangeType](#enum-dynamicrangetype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(DynamicRangeType)

```cangjie
public operator func ==(other: DynamicRangeType): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[DynamicRangeType](#enum-dynamicrangetype)|Yes|-|Another enum value.|

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
```## enum MemberType

```cangjie
public enum MemberType {
    | Int64Value(Int64)
    | StringValue(String)
    | BoolValue(Bool)
}
```

**Description:** Member type of PhotoAsset.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### BoolValue(Bool)

```cangjie
BoolValue(Bool)
```

**Description:** Boolean type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Int64Value(Int64)

```cangjie
Int64Value(Int64)
```

**Description:** Int64 type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### StringValue(String)

```cangjie
StringValue(String)
```

**Description:** String type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

## enum NotifyType

```cangjie
public enum NotifyType <: Equatable<NotifyType> & ToString {
    | NotifyAdd
    | NotifyUpdate
    | NotifyRemove
    | NotifyAlbumAddAsset
    | NotifyAlbumRemoveAsset
    | ...
}
```

**Description:** Type of notification events.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- Equatable\<NotifyType>
- ToString

### NotifyAdd

```cangjie
NotifyAdd
```

**Description:** Notification type for adding a file set or album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### NotifyAlbumAddAsset

```cangjie
NotifyAlbumAddAsset
```

**Description:** Notification type for file sets added to an album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### NotifyAlbumRemoveAsset

```cangjie
NotifyAlbumRemoveAsset
```

**Description:** Notification type for file sets removed from an album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### NotifyRemove

```cangjie
NotifyRemove
```

**Description:** Notification type for removing a file set or album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### NotifyUpdate

```cangjie
NotifyUpdate
```

**Description:** Notification type for updating a file set or album.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(NotifyType)

```cangjie
public operator func !=(other: NotifyType): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[NotifyType](#enum-notifytype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(NotifyType)

```cangjie
public operator func ==(other: NotifyType): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[NotifyType](#enum-notifytype)|Yes|-|Another enum value.|

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

## enum PhotoKeys

```cangjie
public enum PhotoKeys <: ToString & Equatable<PhotoKeys> {
    | Uri
    | PhotoType
    | DisplayName
    | Size
    | DateAdded
    | DateModified
    | Duration
    | Width
    | Height
    | DateTaken
    | Orientation
    | Favorite
    | Title
    | DateAddedMs
    | DateModifiedMs
    | PhotoSubtype
    | DynamicRangeType
    | CoverPosition
    | BurstKey
    | LcdSize
    | ThmSize
    | ...
}
```

**Description:** Key information of photo and video files.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- ToString
- Equatable\<PhotoKeys>

### BurstKey

```cangjie
BurstKey
```

**Description:** Unique identifier for a burst photo set: uuid.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### CoverPosition

```cangjie
CoverPosition
```

**Description:** Cover position of a motion photo, specifically representing the video timestamp (in microseconds) corresponding to the cover frame.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### DateAdded

```cangjie
DateAdded
```

**Description:** Date added (seconds since January 1, 1970).

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### DateAddedMs

```cangjie
DateAddedMs
```

**Description:** Date added (milliseconds since January 1, 1970).

Note: Sorting by this field is not supported when querying photos.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### DateModified

```cangjie
DateModified
```

**Description:** Date modified (seconds since January 1, 1970; modifying the file name does not change this value; it updates only when the file content is modified).

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### DateModifiedMs

```cangjie
DateModifiedMs
```

**Description:** Date modified (milliseconds since January 1, 1970; modifying the file name does not change this value; it updates only when the file content is modified).

Note: Sorting by this field is not supported when querying photos.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### DateTaken

```cangjie
DateTaken
```

**Description:** Date taken (seconds since January 1, 1970).

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### DisplayName

```cangjie
DisplayName
```

**Description:** Display name.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Duration

```cangjie
Duration
```

**Description:** Duration (in milliseconds).

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### DynamicRangeType

```cangjie
DynamicRangeType
```

**Description:** Dynamic range type of the media file.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Favorite

```cangjie
Favorite
```

**Description:** Favorite.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Height

```cangjie
Height
```

**Description:** Image height (in pixels).

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### LcdSize

```cangjie
LcdSize
```

**Description:** Width and height of the LCD image, represented as a string concatenated as width:height.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Orientation

```cangjie
Orientation
```

**Description:** Rotation angle of the file, in degrees.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### PhotoSubtype

```cangjie
PhotoSubtype
```

**Description:** Dynamic range type of the media file.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### PhotoType

```cangjie
PhotoType
```

**Description:** Media file type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Size

```cangjie
Size
```

**Description:** File size (in bytes).

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### ThmSize

```cangjie
ThmSize
```

**Description:** Width and height of the THUMB image, represented as a string concatenated as width:height.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Title

```cangjie
Title
```

**Description:** File title.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Uri

```cangjie
Uri
```

**Description:** File URI.

Note: When querying photos, this field supports only the [DataSharePredicates.equalTo](../ArkData/cj-apis-data_share_predicates.md#func-equaltostring-valuetype) predicate.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Width

```cangjie
Width
```

**Description:** Image width (in pixels).

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(PhotoKeys)

```cangjie
public operator func !=(other: PhotoKeys): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[PhotoKeys](#enum-photokeys)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(PhotoKeys)

```cangjie
public operator func ==(other: PhotoKeys): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[PhotoKeys](#enum-photokeys)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|Description of the enum.|```markdown
## enum PhotoSubtype

```cangjie
public enum PhotoSubtype <: Equatable<PhotoSubtype> & ToString {
    | Default
    | MovingPhoto
    | Burst
    | ...
}
```

**Description:** Burst photo file type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- Equatable\<PhotoSubtype>
- ToString

### Burst

```cangjie
Burst
```

**Description:** Burst photo file type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Default

```cangjie
Default
```

**Description:** Default photo type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### MovingPhoto

```cangjie
MovingPhoto
```

**Description:** Moving photo file type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(PhotoSubtype)

```cangjie
public operator func !=(other: PhotoSubtype): Bool
```

**Description:** Checks whether two enum values are unequal.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PhotoSubtype](#enum-photosubtype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

### func ==(PhotoSubtype)

```cangjie
public operator func ==(other: PhotoSubtype): Bool
```

**Description:** Checks whether two enum values are equal.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PhotoSubtype](#enum-photosubtype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enum. |

## enum PhotoType

```cangjie
public enum PhotoType <: Equatable<PhotoType> & ToString {
    | Image
    | Video
}
```

**Description:** Media file type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- Equatable\<PhotoType>
- ToString

### Image

```cangjie
Image
```

**Description:** Image.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### Video

```cangjie
Video
```

**Description:** Video.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(PhotoType)

```cangjie
public operator func !=(other: PhotoType): Bool 
```

**Description:** Checks whether two enum values are unequal.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PhotoType](#enum-phototype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

### func ==(PhotoType)

```cangjie
public operator func ==(other: PhotoType): Bool 
```

**Description:** Checks whether two enum values are equal.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PhotoType](#enum-phototype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String 
```

**Description:** Gets the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enum. |

## enum PhotoViewMIMETypes

```cangjie
public enum PhotoViewMIMETypes <: Equatable<PhotoViewMIMETypes> & ToString {
    | ImageType
    | VideoType
    | ImageVideoType
    | MovingPhotoImageType
    | ...
}
```

**Description:** Selectable media file types.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- Equatable\<PhotoViewMIMETypes>
- ToString

### ImageType

```cangjie
ImageType
```

**Description:** Image type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### ImageVideoType

```cangjie
ImageVideoType
```

**Description:** Image and video type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### MovingPhotoImageType

```cangjie
MovingPhotoImageType
```

**Description:** Moving photo type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### VideoType

```cangjie
VideoType
```

**Description:** Video type.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(PhotoViewMIMETypes)

```cangjie
public operator func !=(other: PhotoViewMIMETypes): Bool
```

**Description:** Checks whether two enum values are unequal.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PhotoViewMIMETypes](#enum-photoviewmimetypes) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

### func ==(PhotoViewMIMETypes)

```cangjie
public operator func ==(other: PhotoViewMIMETypes): Bool
```

**Description:** Checks whether two enum values are equal.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PhotoViewMIMETypes](#enum-photoviewmimetypes) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enum. |

## enum RecommendationType

```cangjie
public enum RecommendationType <: Equatable<RecommendationType> & ToString {
    | QrOrBarCode
    | QrCode
    | BarCode
    | IdCard
    | ProfilePicture
    | PassPort
    | BankCard
    | DriverLicense
    | DrivingLicense
    | FeaturedSinglePortrait
    | ...
}
```

**Description:** Recommended image types.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- Equatable\<RecommendationType>
- ToString

### BankCard

```cangjie
BankCard
```

**Description:** Bank card.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### BarCode

```cangjie
BarCode
```

**Description:** Barcode.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### DriverLicense

```cangjie
DriverLicense
```

**Description:** Driver's license.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### DrivingLicense

```cangjie
DrivingLicense
```

**Description:** Vehicle license.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### FeaturedSinglePortrait

```cangjie
FeaturedSinglePortrait
```

**Description:** Recommended portrait.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### IdCard

```cangjie
IdCard
```

**Description:** ID card.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### PassPort

```cangjie
PassPort
```

**Description:** Passport.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### ProfilePicture

```cangjie
ProfilePicture
```

**Description:** Profile picture.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### QrCode

```cangjie
QrCode
```

**Description:** QR code.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### QrOrBarCode

```cangjie
QrOrBarCode
```

**Description:** QR code or barcode.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(RecommendationType)

```cangjie
public operator func !=(other: RecommendationType): Bool
```

**Description:** Checks whether two enum values are unequal.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RecommendationType](#enum-recommendationtype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

### func ==(RecommendationType)

```cangjie
public operator func ==(other: RecommendationType): Bool
```

**Description:** Checks whether two enum values are equal.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RecommendationType](#enum-recommendationtype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enum. |
```## enum ResourceType

```cangjie
public enum ResourceType <: Equatable<ResourceType> & ToString {
    | ImageResource
    | VideoResource
    | ...
}
```

**Function:** Represents image resources.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

**Parent Types:**

- Equatable\<ResourceType>
- ToString

### ImageResource

```cangjie
ImageResource
```

**Function:** Represents image resources.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### VideoResource

```cangjie
VideoResource
```

**Function:** Represents video resources.

**System Capability:** SystemCapability.FileManagement.PhotoAccessHelper.Core

**Since:** 22

### func !=(ResourceType)

```cangjie
public operator func !=(other: ResourceType): Bool
```

**Function:** Determines whether two enum values are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ResourceType](#enum-resourcetype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are not equal, otherwise returns false.|

### func ==(ResourceType)

```cangjie
public operator func ==(other: ResourceType): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ResourceType](#enum-resourcetype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the value of the enum.

**Return Value:**

|Type|Description|
|:----|:----|
|String|The description of the enum.|