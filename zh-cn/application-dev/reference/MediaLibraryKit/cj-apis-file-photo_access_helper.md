# ohos.file.photo_access_helper

该模块提供相册管理模块能力，包括创建相册以及访问、修改相册中的媒体数据信息等。

## 导入模块

```cangjie
import kit.MediaLibraryKit.*
```

## 权限列表

ohos.permission.READ_IMAGEVIDEO

ohos.permission.WRITE_IMAGEVIDEO

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func getPhotoAccessHelper(UIAbilityContext)

```cangjie
public func getPhotoAccessHelper(context: UIAbilityContext): PhotoAccessHelper
```

**功能：** 获取相册管理模块的实例，用于访问和修改相册中的媒体文件。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|传入Ability实例的Context。|

**返回值：**

|类型|说明|
|:----|:----|
|[PhotoAccessHelper](./cj-apis-file-photo_access_helper.md#class-photoaccesshelper)|相册管理模块的实例。|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*

let ctx = Global.getAbilityContext() // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
```

## interface MediaChangeRequest

```cangjie
public interface MediaChangeRequest {}
```

**功能：** 媒体变更请求，资产变更请求和相册变更请求的父类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

## class AbsAlbum

```cangjie
public open class AbsAlbum {}
```

**功能：** AbsAlbum模块。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### prop albumName

```cangjie
public mut prop albumName: String
```

**功能：** 相册名称。预置相册不可写，用户相册可写。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### prop albumSubtype

```cangjie
public prop albumSubtype: AlbumSubtype
```

**功能：** 相册子类型。

**类型：** [AlbumSubtype](#enum-albumsubtype)

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### prop albumType

```cangjie
public prop albumType: AlbumType
```

**功能：** 相册类型。

**类型：** [AlbumType](#enum-albumtype)

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### prop albumUri

```cangjie
public prop albumUri: String
```

**功能：** 相册uri。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### prop count

```cangjie
public prop count: Int32
```

**功能：** 相册中文件数量。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### prop coverUri

```cangjie
public prop coverUri: String
```

**功能：** 封面文件uri。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func getAssets(FetchOptions)

```cangjie
public func getAssets(options: FetchOptions): PhotoAssetResult
```

**功能：** 获取相册中的文件。

**需要权限：** ohos.READ_IMAGEVIDEO

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|options|[FetchOptions](./cj-apis-file-photo_access_helper.md#class-fetchoptions)|是|-| 检索选项。|

**返回值：**

|类型|说明|
|:----|:----|
|[PhotoAssetResult](#class-photoassetresult)|返回图片和视频数据结果集。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;2. Incorrect parameter types; 3. Parameter verification failed. |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

## class Album

```cangjie
public class Album <: AbsAlbum {}
```

**功能：** 实体相册。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- [AbsAlbum](#class-absalbum)

### prop imageCount

```cangjie
public prop imageCount: Int32
```

**功能：** 获取相册中图片数量。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### prop videoCount

```cangjie
public prop videoCount: Int32
```

**功能：** 获取相册中图片数量。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func commitModify()

```cangjie
public func commitModify(): Unit
```

**功能：** 更新相册属性修改到数据库中。

**需要权限：** ohos.WRITE_IMAGEVIDEO

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;2. Incorrect parameter types. |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.getAbilityContext() // 需获取Context应用上下文，详见本文使用说明
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

**功能：** 相册结果模块。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- [FetchResult](#class-fetchresult)

### func getAllObjects()

```cangjie
public func getAllObjects(): Array<Album>
```

**功能：** 获取相册中的所有资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Array\<[Album](#class-album)>|返回相册列表。|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.getAbilityContext() // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
predicates.equalTo('album_name', Str('test1'))
let fetchOptions: FetchOptions = FetchOptions(fetchColumns: [], predicates: predicates)
let fetchResult: FetchResult<Album> = phAccessHelper.getAlbums(AlbumType.USER,
    AlbumSubtype.USER_GENERIC, options: fetchOptions)
let albums = fetchResult.getAllObjects()
```  

### func getFirstObject()

```cangjie
public func getFirstObject(): Album
```

**功能：** 获取相册中的第一个文件资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[Album](#class-album)|返回第一个相册|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |\

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.getAbilityContext() // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
predicates.equalTo('album_name', Str('test1'))
let fetchOptions: FetchOptions = FetchOptions(fetchColumns: [], predicates: predicates)
let fetchResult: FetchResult<Album> = phAccessHelper.getAlbums(AlbumType.USER,
    AlbumSubtype.USER_GENERIC, options: fetchOptions)
let album = fetchResult.getFirstObject()
```  

### func getLastObject()

```cangjie
public func getLastObject(): Album
```

**功能：** 获取相册中的最后一个文件资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[Album](#class-album)|返回最后一个相册。|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.getAbilityContext() // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
predicates.equalTo('album_name', Str('test1'))
let fetchOptions: FetchOptions = FetchOptions(fetchColumns: [], predicates: predicates)
let fetchResult: FetchResult<Album> = phAccessHelper.getAlbums(AlbumType.USER,
    AlbumSubtype.USER_GENERIC, options: fetchOptions)
let album = fetchResult.getLastObject()
```  

### func getNextObject()

```cangjie
public func getNextObject(): Album
```

**功能：** 获取相册中的下一个文件资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[Album](#class-album)|返回下一个相册|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.getAbilityContext() // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
predicates.equalTo('album_name', Str('test1'))
let fetchOptions: FetchOptions = FetchOptions(fetchColumns: [], predicates: predicates)
let fetchResult: FetchResult<Album> = phAccessHelper.getAlbums(AlbumType.USER,
    AlbumSubtype.USER_GENERIC, options: fetchOptions)
let album = fetchResult.getNextObject()
``` 

### func getObjectByPosition(Int32)

```cangjie
public func getObjectByPosition(index: Int32): Album
```

**功能：** 获取文件检索结果中具有指定索引的文件资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|index|Int32|是|-|要获取的文件的索引，从0开始。|

**返回值：**

|类型|说明|
|:----|:----|
|[Album](#class-album)|获取的文件资产。|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.getAbilityContext() // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
predicates.equalTo('album_name', Str('test1'))
let fetchOptions: FetchOptions = FetchOptions(fetchColumns: [], predicates: predicates)
let fetchResult: FetchResult<Album> = phAccessHelper.getAlbums(AlbumType.USER,
    AlbumSubtype.USER_GENERIC, options: fetchOptions)
let album = fetchResult.getObjectByPosition(0)
``` 

## class ChangeData

```cangjie
public class ChangeData {
    public var notifyType: NotifyType
    public var uris: Array<String>
    public var extraUris: Array<String>
}
```

**功能：** 监听器回调函数的值。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var extraUris

```cangjie
public var extraUris: Array<String>
```

**功能：** 相册中变动文件的uri数组。

**类型：** Array\<String>

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var notifyType

```cangjie
public var notifyType: NotifyType
```

**功能：** ChangeData的通知类型。

**类型：** [NotifyType](#enum-notifytype)

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var uris

```cangjie
public var uris: Array<String>
```

**功能：** 相同[NotifyType](#enum-notifytype)的所有uri，可以是PhotoAsset或Album。。

**类型：** Array\<String>

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

## class CreateOptions

```cangjie
public class CreateOptions {
    public var title: String = ""
    public var subtype: PhotoSubtype
    public init(title!: String = "", subtype!: PhotoSubtype = Default)
}
```

**功能：** 图片或视频的创建选项。

title参数规格为：

- 不应包含扩展名。
- 文件名字符串长度为1~255。
- 文件名中不允许出现的非法英文字符，包括：. .. \ / : * ? " ' ` < > | { } [ ]

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var subtype

```cangjie
public var subtype: PhotoSubtype
```

**功能：** 图片或者视频的标题。

**类型：** [PhotoSubtype](#enum-photosubtype)

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var title

```cangjie
public var title: String = ""
```

**功能：** 图片或者视频的标题。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### init(String, PhotoSubtype)

```cangjie
public init(title!: String = "", subtype!: PhotoSubtype = Default)
```

**功能：** 构造CreateOptions对象。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|title|String|否|""| **命名参数。** 图片或者视频的标题。|
|subtype|[PhotoSubtype](#enum-photosubtype)|否|Default| **命名参数。** 图片或者视频的文件子类型。|

## class FetchOptions

```cangjie
public class FetchOptions {
    public var fetchColumns: Array<String>
    public var predicates: DataSharePredicates
    public init(fetchColumns: Array<String>, predicates: DataSharePredicates)
}
```

**功能：** 检索条件。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var fetchColumns

```cangjie
public var fetchColumns: Array<String>
```

**功能：** 检索条件。

**类型：** Array\<String>

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var predicates

```cangjie
public var predicates: DataSharePredicates
```

**功能：** 谓词查询。

**类型：** [DataSharePredicates](../ArkData/cj-apis-data_share_predicates.md#class-datasharepredicates)

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### init(Array\<String>, DataSharePredicates)

```cangjie
public init(fetchColumns: Array<String>, predicates: DataSharePredicates)
```

**功能：** 构造FetchOptions对象。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|fetchColumns|Array\<String>|是|-| 检索条件，指定列名查询。<br>对于照片，如果该参数为空，默认查询'uri'、'media_type'、'subtype'和'display_name'。示例：fetchColumns: ['uri', 'title']。<br>对于相册，如果该参数为空，默认查询'uri'和'album_name'。|
|predicates|[DataSharePredicates](../ArkData/cj-apis-data_share_predicates.md#class-datasharepredicates)|是|-| 谓词查询，显示过滤条件。|

## class FetchResult

```cangjie
public open class FetchResult {}
```

**功能：** 文件检索结果集。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func close()

```cangjie
public func close(): Unit
```

**功能：** 释放FetchResult实例并使其失效。无法调用其他方法。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
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

**功能：** 获取文件检索结果中的文件总数。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Int32|检索到的文件总数。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
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

**功能：** 检查结果集是否指向最后一行。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Bool|当读到最后一条记录后，后续没有记录返回true，否则返回false。|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult: PhotoAccessResult = phAccessHelper.getAssets(fetchOptions)
let isAfterLast = fetchResult.isAfterLast()
```

## class MediaAlbumChangeRequest

```cangjie
public class MediaAlbumChangeRequest <: MediaChangeRequest {
    public init(album: Album)
}
```

**功能：** 相册变更请求。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- [MediaChangeRequest](#interface-mediachangerequest)

### init(Album)

```cangjie
/**
 * The constructor to create a MediaAlbumChangeRequest instance.
 *
 * @throws { BusinessException } 401 - Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;
 * <br>2. Incorrect parameter types; 3. Parameter verification failed.
 * @throws { BusinessException } 14000011 - System inner fail
 * @relation constructor(album: Album)
 */
public init(album: Album)
```

**功能：** 构造MediaAlbumChangeRequest对象。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|album|[Album](./cj-apis-file-photo_access_helper.md#class-album)|是|-|需要变更的相册。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult = phAccessHelper.getAlbums(AlbumType.User, AlbumSubtype.UserGeneric,
    options: fetchOptions)
let album = fetchResult.getFirstObject()
let albumChangeRequest = MediaAlbumChangeRequest(album)
```

### func addAssets(Array\<PhotoAsset>)

```cangjie
public func addAssets(assets: Array<PhotoAsset>): Unit
```

**功能：** 向相册中添加资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|assets|Array\<[PhotoAsset](./cj-apis-file-photo_access_helper.md#class-photoasset)>|是|-|待添加到相册中的资产数组。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult = phAccessHelper.getAssets(fetchOptions)
let asset = fetchResult.getFirstObject()
let albumFetchResult = phAccessHelper.getAlbums(AlbumType.User, AlbumSubtype.UserGeneric)
let album = albumFetchResult.getFirstObject()
let albumChangeRequest = MediaAlbumChangeRequest(album)
albumChangeRequest.addAssets([asset, asset])
```

### func getAlbum()

```cangjie
public func getAlbum(): Album
```

**功能：** 获取当前相册变更请求中的相册。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[Album](./cj-apis-file-photo_access_helper.md#class-album)|返回当前相册变更请求中的相册。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult = phAccessHelper.getAlbums(AlbumType.User, AlbumSubtype.UserGeneric,
    options: fetchOptions)
let album = fetchResult.getFirstObject()
let albumChangeRequest = MediaAlbumChangeRequest(album)
var changeRequestAlbum = albumChangeRequest.getAlbum()
```

### func removeAssets(Array\<PhotoAsset>)

```cangjie
public func removeAssets(assets: Array<PhotoAsset>): Unit
```

**功能：** 从相册中移除资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|assets|Array\<[PhotoAsset](./cj-apis-file-photo_access_helper.md#class-photoasset)>|是|-|待从相册中移除的资产数组。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
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
```

### func setAlbumName(String)

```cangjie
public func setAlbumName(name: String): Unit
```

**功能：** 设置相册名称。

相册名的参数规格为

- 相册名字符串长度为1~255。
- 不允许出现非法字符，包括：. .. \ / : * ? " ' ` < > | { } [ ]
- 英文字符大小写不敏感。
- 相册名不允许重名。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|待设置的相册名称。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult = phAccessHelper.getAlbums(AlbumType.User, AlbumSubtype.UserGeneric,
    options: fetchOptions)
let album = fetchResult.getFirstObject()
let albumChangeRequest = MediaAlbumChangeRequest(album)
let newAlbumName = "newAAA"
albumChangeRequest.setAlbumName(newAlbumName)
```

## class MediaAssetChangeRequest

```cangjie
public class MediaAssetChangeRequest <: & MediaChangeRequest {
    public init(asset: PhotoAsset)
}
```

**功能：** 资产变更请求。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- [MediaChangeRequest](#interface-mediachangerequest)

### init(PhotoAsset)

```cangjie
public init(asset: PhotoAsset)
```

**功能：** 构造MediaAssetChangeRequest对象。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|asset|[PhotoAsset](./cj-apis-file-photo_access_helper.md#class-photoasset)|是|-|需要变更的资产。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions = FetchOptions([], predicates)
let fetchResult = phAccessHelper.getAssets(fetchOptions)
let photoAsset = fetchResult.getFirstObject()
let assetChangeRequest = MediaAssetChangeRequest(photoAsset)
```

### static func createAssetRequest(UIAbilityContext, PhotoType, String, CreateOptions)

```cangjie
public static func createAssetRequest(context: UIAbilityContext, photoType: PhotoType, extension: String,
    options!: CreateOptions = CreateOptions(title: "", subtype: Default)): MediaAssetChangeRequest
```

**功能：** 指定待创建的文件类型和扩展名，创建资产变更请求。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|传入Ability实例的Context。|
|photoType|[PhotoType](./cj-apis-file-photo_access_helper.md#enum-phototype)|是|-|待创建的文件类型，IMAGE或者VIDEO类型。|
|extension|String|是|-|文件扩展名，例如：'jpg'。|
|options|[CreateOptions](#class-createoptions)|否|CreateOptions(title: "", subtype: Default)|**命名参数。** 创建选项，例如：{title: 'testPhoto'}。|

**返回值：**

|类型|说明|
|:----|:----|
|[MediaAssetChangeRequest](#class-mediaassetchangerequest)|返回创建资产的变更请求。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let photoType = PhotoType.Image
let extension = "jpg"
let options = CreateOptions(title: "testPhoto")
let assetChangeRequest = MediaAssetChangeRequest.createAssetRequest(ctx, photoType,
    extension, options: options)
```

### static func createImageAssetRequest(UIAbilityContext, String)

```cangjie
public static func createImageAssetRequest(context: UIAbilityContext, fileUri: String): MediaAssetChangeRequest
```

**功能：** 创建图片资产变更请求。

通过fileUri指定待创建资产的数据来源，可参考[FileUri](../CoreFileKit/cj-apis-file_fileuri.md)。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|传入Ability实例的Context。|
|fileUri|String|是|-|图片资产的数据来源，在应用沙箱下的uri。|

**返回值：**

|类型|说明|
|:----|:----|
|[MediaAssetChangeRequest](#class-mediaassetchangerequest)|返回创建资产的变更请求。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 13900002 | The file corresponding to the URI is not in the app sandbox. |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let fileUri = "file://com.example.xxx/data/storage/el2/base/haps/entry/files/test.jpg"
let assetChangeRequest = MediaAssetChangeRequest.createImageAssetRequest(ctx,
    fileUri)
phAccessHelper.applyChanges(assetChangeRequest)
```

### static func createVideoAssetRequest(UIAbilityContext, String)

```cangjie
public static func createVideoAssetRequest(context: UIAbilityContext, fileUri: String): MediaAssetChangeRequest
```

**功能：** 创建视频资产变更请求。

通过fileUri指定待创建资产的数据来源，可参考[FileUri](../CoreFileKit/cj-apis-file_fileuri.md)。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|传入Ability实例的Context。|
|fileUri|String|是|-|视频资产的数据来源，在应用沙箱下的uri。|

**返回值：**

|类型|说明|
|:----|:----|
|[MediaAssetChangeRequest](#class-mediaassetchangerequest)|返回创建资产的变更请求。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 13900002 | The file corresponding to the URI is not in the app sandbox. |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let fileUri = "file://com.example.xxx/data/storage/el2/base/haps/entry/files/test.mp4"
let assetChangeRequest = MediaAssetChangeRequest.createVideoAssetRequest(ctx,
    fileUri)
phAccessHelper.applyChanges(assetChangeRequest)
```

### static func deleteAssets(UIAbilityContext, Array\<PhotoAsset>)

```cangjie
public static func deleteAssets(context: UIAbilityContext, assets: Array<PhotoAsset>): Unit
```

**功能：** 删除媒体文件，删除的文件进入到回收站。

**需要权限：** ohos.permission.WRITE_IMAGEVIDEO

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|传入Ability实例的Context。|
|assets|Array\<[PhotoAsset](./cj-apis-file-photo_access_helper.md#class-photoasset)>|是|-|待删除的媒体文件uri数组。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult = phAccessHelper.getAssets(fetchOptions)
let asset = fetchResult.getFirstObject()
MediaAssetChangeRequest.deleteAssets(ctx, asset.uri)
```

### static func deleteAssets(UIAbilityContext, Array\<String>)

```cangjie
public static func deleteAssets(context: UIAbilityContext, assets: Array<String>): Unit
```

**功能：** 删除媒体文件，删除的文件进入到回收站。

**需要权限：** ohos.permission.WRITE_IMAGEVIDEO

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|传入Ability实例的Context。|
|assets|Array\<String>|是|-|待删除的媒体文件uri数组。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14000002 | The uri format is incorrect or does not exist. |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult = phAccessHelper.getAssets(fetchOptions)
let asset = fetchResult.getFirstObject()
MediaAssetChangeRequest.deleteAssets(ctx, asset.uri)
```

### func addResource(ResourceType, String)

```cangjie
public func addResource(resourceType: ResourceType, fileUri: String): Unit
```

**功能：** 通过ArrayBuffer数据添加资源。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|resourceType|[ResourceType](#enum-resourcetype)|是|-|待添加资源的类型。|
|fileUri|String|是|-|待添加资源的数据来源，在应用沙箱下的uri。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 13900002 | The file corresponding to the URI is not in the app sandbox. |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let photoType = PhotoType.Image
let extension = "jpg"
let assetChangeRequest = MediaAssetChangeRequest.createAssetRequest(ctx, photoType,
    extension)
let buffer = Array<Byte>(2048, repeat: 0)
assetChangeRequest.addResource(ResourceType.ImageResource, buffer)
phAccessHelper.applyChanges(assetChangeRequest)
```

### func addResource(ResourceType, Array\<Byte>)

```cangjie
public func addResource(resourceType: ResourceType, data: Array<Byte>): Unit
```

**功能：** 通过ArrayBuffer数据添加资源。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|resourceType|[ResourceType](#enum-resourcetype)|是|-|待添加资源的类型。|
|data|Array\<Byte>|是|-|待添加资源的数据。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let photoType = PhotoType.Image
let extension = "jpg"
let assetChangeRequest = MediaAssetChangeRequest.createAssetRequest(ctx, photoType,
    extension)
let buffer = Array<Byte>(2048, repeat: 0)
assetChangeRequest.addResource(ResourceType.ImageResource, buffer)
phAccessHelper.applyChanges(assetChangeRequest)
```

### func discardCameraPhoto()

```cangjie
public func discardCameraPhoto(): Unit
```

**功能：** 保存相机拍摄的照片。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 14000011 | Internal system error |
  | 14000016 | Operation Not Support |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions = FetchOptions([], predicates)
let fetchResult = phAccessHelper.getAssets(fetchOptions)
let photoAsset = fetchResult.getFirstObject()
let assetChangeRequest = MediaAssetChangeRequest(photoAsset)
assetChangeRequest.discardCameraPhoto()
phAccessHelper.applyChanges(assetChangeRequest)
```

### func getAsset()

```cangjie
public func getAsset(): PhotoAsset
```

**功能：** 获取当前资产变更请求中的资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[PhotoAsset](./cj-apis-file-photo_access_helper.md#class-photoasset)|返回当前资产变更请求中的资产。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult = phAccessHelper.getAssets(fetchOptions)
let photoAsset = fetchResult.getFirstObject()
let assetChangeRequest = MediaAssetChangeRequest(photoAsset)
let asset = assetChangeRequest.getAsset()
```

### func getWriteCacheHandler()

```cangjie
public func getWriteCacheHandler(): Int32
```

**功能：** 获取临时文件写句柄。

**需要权限：** ohos.permission.WRITE_IMAGEVIDEO

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Int32|返回临时文件写句柄。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.CoreFileKit.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let assetChangeRequest = MediaAssetChangeRequest.createAssetRequest(ctx,
    PhotoType.Video, "mp4")
let fd = assetChangeRequest.getWriteCacheHandler()
FileIo.close(fd)
phAccessHelper.applyChanges(assetChangeRequest)
```

### func saveCameraPhoto()

```cangjie
public func saveCameraPhoto(): Unit
```

**功能：** 保存相机拍摄的照片。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 14000011 | System inner fail |
  | 14000016 | Operation Not Support |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions = FetchOptions([], predicates)
let fetchResult = phAccessHelper.getAssets(fetchOptions)
let photoAsset = fetchResult.getFirstObject()
let assetChangeRequest = MediaAssetChangeRequest(photoAsset)
assetChangeRequest.saveCameraPhoto()
phAccessHelper.applyChanges(assetChangeRequest)
```

### func setTitle(String)

```cangjie
public func setTitle(title: String): Unit
```

**功能：** 修改媒体资产的标题。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|title|String|是|-|待修改的资产标题。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult = phAccessHelper.getAssets(fetchOptions)
let photoAsset = fetchResult.getFirstObject()
let assetChangeRequest = MediaAssetChangeRequest(photoAsset)
let newTitle = "newTitle"
assetChangeRequest.setTitle(newTitle)
phAccessHelper.applyChanges(assetChangeRequest)
```

## class PhotoAccessHelper

```cangjie
public class PhotoAccessHelper {}
```

**功能：** 获取图片和视频资源。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func applyChanges(MediaChangeRequest)

```cangjie
public func applyChanges(mediaChangeRequest: MediaChangeRequest): Unit
```

**功能：** 提交媒体变更请求。

**需要权限：** ohos.WRITE_IMAGEVIDEO

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|mediaChangeRequest|[MediaChangeRequest](#interface-mediachangerequest)|是|-|媒体变更请求，支持资产变更请求和相册变更请求。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14000011 | System inner fail |

### func getAlbums(AlbumType, AlbumSubtype, FetchOptions)

```cangjie
public func getAlbums(albumType: AlbumType, subtype: AlbumSubtype,
    options!: FetchOptions = FetchOptions(["uri", "album_name"], DataSharePredicates())): AlbumResult
```

**功能：** 根据检索选项和相册类型获取相册。获取相册前需先保证相册存在。

**需要权限：** ohos.READ_IMAGEVIDEO

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|albumType|[AlbumType](#enum-albumtype)|是|-|相册类型。|
|subtype|[AlbumSubtype](#enum-albumsubtype)|是|-|相册子类型。|
|options|[FetchOptions](#class-fetchoptions)|否|FetchOptions(["uri", "album_name"], DataSharePredicates())|**命名参数。** 检索选项。|

**返回值：**

|类型|说明|
|:----|:----|
|AlbumResult|返回获取相册的结果集。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult: AlbumResult = phAccessHelper.getAlbums(AlbumType.User,
    AlbumSubtype.UserGeneric, options: fetchOptions)
```

### func getAssets(FetchOptions)

```cangjie
public func getAssets(options: FetchOptions): PhotoAssetResult
```

**功能：** 获取图片和视频资源。

**需要权限：** ohos.READ_IMAGEVIDEO

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|options|[FetchOptions](#class-fetchoptions)|是|-|图片和视频检索选项。|

**返回值：**

|类型|说明|
|:----|:----|
|PhotoAssetResult|返回获取连拍照片的结果集。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult: PhotoAssetResult = phAccessHelper.getAssets(fetchOptions)
```

### func getBurstAssets(String, FetchOptions)

```cangjie
public func getBurstAssets(burstKey: String, options: FetchOptions): PhotoAssetResult
```

**功能：** 获取连拍照片资源。

**需要权限：** ohos.READ_IMAGEVIDEO

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|burstKey|String|是|-|一组连拍照片的唯一标识：uuid(可传入[PhotoKeys](#enum-photokeys)的BURST_KEY)。|
|options|[FetchOptions](#class-fetchoptions)|是|-|连拍照片检索选项。|

**返回值：**

|类型|说明|
|:----|:----|
|PhotoAssetResult|返回获取连拍照片的结果集。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied |
  | 14000011 | Internal system error |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let burstKey = YOUR_UUID // 请输入uuid
let fetchResult: PhotoAssetResult = phAccessHelper.getBurstAssets(burstKey, fetchOptions)
```

### func registerChange(String, Bool, Callback1Argument\<ChangeData>)

```cangjie
public func registerChange(uri: String, forChildUris: Bool, callback: Callback1Argument<ChangeData>): Unit
```

**功能：** 注册对指定uri的监听，使用callback方式返回异步结果。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|uri|String|是|-|PhotoAsset的uri, Album的uri或[DefaultChangeUri](#enum-defaultchangeuri)的值。|
|forChildUris|Bool|是|-|是否模糊监听，uri为相册uri时，forChildUris为true能监听到相册中文件的变化，如果是false只能监听相册本身变化。uri为photoAsset时，forChildUris为true、false没有区别，uri为DefaultChangeUri时，forChildUris必须为true，如果为false将找不到该uri，收不到任何消息。|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[ChangeData](#class-changedata)>|是|-|返回要监听的[ChangeData](#class-changedata)。注：uri可以注册多个不同的callback监听，[unRegisterChange](#func-unregisterchangestring-callback1argumentchangedata)可以关闭该uri所有监听，也可以关闭指定callback的监听。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 13900012 | Permission denied |
  | 13900020 | Invalid argument |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

import ohos.base.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

// 此处代码可添加在依赖项定义中
class MyCallback<T> <: Callback1Argument<T> {
    public let callabck_: (T) -> Unit
    public init(callabck: (T) -> Unit) {
        callabck_ = callabck
    }
    public open func invoke(err: ?BusinessException, arg: T): Unit {
        callabck_(arg)
    }
}

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
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
```

### func release()

```cangjie
public func release(): Unit
```

**功能：** 释放PhotoAccessHelper实例。当后续不需要使用PhotoAccessHelper 实例中的方法时调用。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
let phAccessHelper = getPhotoAccessHelper(ctx)
let predicates = DataSharePredicates()
let fetchOptions: FetchOptions = FetchOptions([], predicates)
let fetchResult: PhotoAssetResult = phAccessHelper.getAssets(fetchOptions)
fetchResult.close()
phAccessHelper.release()
```

### func showAssetsCreationDialog(Array\<String>, Array\<PhotoCreationConfig>, Callback1Argument\<Array\<String>>)

```cangjie
public func showAssetsCreationDialog(srcFileUris: Array<String>, photoCreationConfigs: Array<PhotoCreationConfig>,
    callback: Callback1Argument<Array<String>>): Unit
```

**功能：** 调用接口拉起保存确认弹窗。用户同意保存后，在callback中返回已创建并授予保存权限的uri列表，该列表永久生效，应用可使用该uri写入图片/视频。如果用户拒绝保存，将返回空列表。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|srcFileUris|Array\<String>|是|-|需保存到媒体库中的图片/视频文件对应的媒体库uri。<br>**注意：**  仅支持处理图片、视频uri。|
|photoCreationConfigs|Array\<[PhotoCreationConfig](#class-photocreationconfig)>|是|-|保存图片/视频到媒体库的配置，包括保存的文件名等，与srcFileUris保持一一对应。|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<Array\<String>>|是|-|回调函数，获取返回给应用的媒体库文件uri列表。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14000011 | Internal system error |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

import ohos.base.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

// 此处代码可添加在依赖项定义中
class MyCallback<T> <: Callback1Argument<T> {
    public let callabck_: (T) -> Unit
    public init(callabck: (T) -> Unit) {
        callabck_ = callabck
    }
    public open func invoke(err: ?BusinessException, arg: T): Unit {
        callabck_(arg)
    }
}

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
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
// 获取需要保存到媒体库的位于应用沙箱的图片/视频uri
// 实际场景请使用真实的uri
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
```

### func unRegisterChange(String, ?Callback1Argument\<ChangeData>)

```cangjie
public func unRegisterChange(uri: String, callback!: ?Callback1Argument<ChangeData> = None): Unit
```

**功能：** 取消指定uri的监听，一个uri可以注册多个监听，存在多个callback监听时，可以取消指定注册的callback的监听；不指定callback时取消该uri的所有监听。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|uri|String|是|-|PhotoAsset的uri, Album的uri或[DefaultChangeUri](#enum-defaultchangeuri)的值。|
|callback|?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[ChangeData](#class-changedata)>|否|None|**命名参数。** 取消[registerChange](#func-registerchangestring-bool-callback1argumentchangedata)注册时的callback的监听，不填时，取消该uri的所有监听。注：off指定注册的callback后不会进入此回调。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 13900012 | Permission denied |
  | 13900020 | Invalid argument |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*

import ohos.base.*
import ohos.callback_invoke.*
import ohos.business_exception.BusinessException

// 此处代码可添加在依赖项定义中
class MyCallback<T> <: Callback1Argument<T> {
    public let callabck_: (T) -> Unit
    public init(callabck: (T) -> Unit) {
        callabck_ = callabck
    }
    public open func invoke(err: ?BusinessException, arg: T): Unit {
        callabck_(arg)
    }
}

let ctx = Global.abilityContext // 需获取Context应用上下文，详见本文使用说明
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
```

## class PhotoAsset

```cangjie
public class PhotoAsset {}
```

**功能：** 提供封装文件属性的方法。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### prop displayName

```cangjie
public prop displayName: String
```

**功能：** 获取文件名，包含后缀名。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### prop photoType

```cangjie
public prop photoType: PhotoType
```

**功能：** 获取媒体文件类型。

**类型：** [PhotoType](#enum-phototype)

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### prop uri

```cangjie
public prop uri: String
```

**功能：** 获取媒体文件资源uri。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func commitModify()

```cangjie
public func commitModify(): Unit
```

**功能：** 修改文件的元数据。

**需要权限：** ohos.permission.WRITE_IMAGEVIDEO

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;2. Incorrect parameter types. |
  | 201 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000001 | Invalid display name |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.*

let ctx = Global.getAbilityContext() // 需获取Context应用上下文，详见本文使用说明
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

**功能：** 获取PhotoAsset成员参数。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|member|String|是|-|成员参数名称，在get时，除了'uri'、'media_type'、'subtype'和'display_name'四个属性之外，其他的属性都需要在fetchColumns中填入需要get的[PhotoKeys](./cj-apis-file-photo_access_helper.md#enum-photokeys)，例如：get title属性fetchColumns: ['title']。|

**返回值：**

|类型|说明|
|:----|:----|
|[MemberType](#enum-membertype)|获取PhotoAsset成员参数的值。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;2. Incorrect parameter types; 3. Parameter verification failed. |
  | 13900020 | Invalid argument |
  | 14000014 | The provided member must be a property name of PhotoKey. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.*

let ctx = Global.getAbilityContext() // 需获取Context应用上下文，详见本文使用说明
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

**功能：** 获取文件的缩略图，传入缩略图尺寸。

**需要权限：** ohos.permission.WRITE_IMAGEVIDEO

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|size|?[Size](../ImageKit/cj-apis-image.md#class-size)|否|Size(256, 256)|**命名参数。** 缩略图尺寸。|

**返回值：**

|类型|说明|
|:----|:----|
|[PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap)|返回缩略图的PixelMap。|


**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;2. Incorrect parameter types; 3. Parameter verification failed. |
  | 13900012 | Permission denied |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.*

let ctx = Global.getAbilityContext() // 需获取Context应用上下文，详见本文使用说明
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

**功能：** 设置PhotoAsset成员参数。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|member|String|是|-|成员参数名称例如：[PhotoKeys](./cj-apis-file-photo_access_helper.md#enum-photokeys).TITLE。|
|value|String|是|-|设置成员参数名称，只能修改[PhotoKeys](./cj-apis-file-photo_access_helper.md#enum-photokeys).TITLE的值。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;2. Incorrect parameter types; 3. Parameter verification failed. |
  | 13900020 | Invalid argument |
  | 14000014 | The provided member must be a property name of PhotoKey. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.*

let ctx = Global.getAbilityContext() // 需获取Context应用上下文，详见本文使用说明
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
```

## class PhotoAssetResult

```cangjie
public class PhotoAssetResult <: FetchResult {}
```

**功能：** 提供封装文件属性的方法。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- [FetchResult](#class-fetchresult)

### func getAllObjects()

```cangjie
public func getAllObjects(): Array<PhotoAsset>
```

**功能：** 获取文件检索结果中的所有文件资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Array\<[PhotoAsset](#class-photoasset)>|返回结果集中所有文件资产数组。|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getFirstObject()

```cangjie
public func getFirstObject(): PhotoAsset
```

**功能：** 获取文件检索结果中的第一个文件资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[PhotoAsset](#class-photoasset)|返回结果集中第一个对象。|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getLastObject()

```cangjie
public func getLastObject(): PhotoAsset
```

**功能：** 获取文件检索结果中的最后一个文件资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[PhotoAsset](#class-photoasset)|返回结果集中最后一个对象。|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getNextObject()

```cangjie
public func getNextObject(): PhotoAsset
```

**功能：** 获取文件检索结果中的下一个文件资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[PhotoAsset](#class-photoasset)|返回结果集中下一个对象。|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 13900020 | Invalid argument |
  | 14000011 | System inner fail |

### func getObjectByPosition(Int32)

```cangjie
public func getObjectByPosition(index: Int32): PhotoAsset
```

**功能：** 获取文件检索结果中具有指定索引的文件资产。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|index|Int32|是|-|要获取的文件的索引，从0开始。|

**返回值：**

|类型|说明|
|:----|:----|
|[PhotoAsset](#class-photoasset)|获取的文件资产。|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](../CoreFileKit/cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
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

**功能：** 保存图片/视频到媒体库的配置，包括保存的文件名等。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var fileNameExtension

```cangjie
public var fileNameExtension: String
```

**功能：** 文件扩展名。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var photoType

```cangjie
public var photoType: PhotoType
```

**功能：** 文件类型。

**类型：** [PhotoType](#enum-phototype)

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var subtype

```cangjie
public var subtype: PhotoSubtype
```

**功能：** 文件子类型。

**类型：** [PhotoSubtype](#enum-photosubtype)

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var title

```cangjie
public var title: String
```

**功能：** 图片或者视频的标题。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### init(String, PhotoType, String, PhotoSubtype)

```cangjie
public init(fileNameExtension: String, photoType: PhotoType, title!: String = "", subtype!: PhotoSubtype = Default)
```

**功能：** 构造PhotoCreationConfig对象。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|fileNameExtension|String|是|-|文件扩展名，例如'jpg'。|
|photoType|[PhotoType](./cj-apis-file-photo_access_helper.md#enum-phototype)|是|-|创建的文件类型，IMAGE或者VIDEO。|
|title|String|否|""| **命名参数。** 图片或者视频的标题。|
|subtype|[PhotoSubtype](#enum-photosubtype)|否|Default| **命名参数。** 图片或者视频的文件子类型，Default或者MovingPhoto。|

## class RequestOptions

```cangjie
public class RequestOptions {
    public var deliveryMode: DeliveryMode
}
```

**功能：** 请求策略。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### var deliveryMode

```cangjie
public var deliveryMode: DeliveryMode
```

**功能：** 请求资源分发模式。

**类型：** [DeliveryMode](#enum-deliverymode)

**读写能力：** 可读写

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

## enum AlbumKeys

```cangjie
public enum AlbumKeys <: ToString & Equatable<AlbumKeys> {
    | Uri
    | AlbumName
    | ...
}
```

**功能：** 相册关键信息。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- ToString
- Equatable\<AlbumKeys>

### AlbumName

```cangjie
AlbumName
```

**功能：** 相册名字。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Uri

```cangjie
Uri
```

**功能：** 相册uri。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(AlbumKeys)

```cangjie
public operator func !=(other: AlbumKeys): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[AlbumKeys](#enum-albumkeys)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(AlbumKeys)

```cangjie
public operator func ==(other: AlbumKeys): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[AlbumKeys](#enum-albumkeys)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

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

**功能：** 相册子类型，表示具体的相册类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- Equatable\<AlbumSubtype>
- ToString

### AnyAlbum

```cangjie
AnyAlbum
```

**功能：** 任意相册。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Favorite

```cangjie
Favorite
```

**功能：** 收藏夹。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Image

```cangjie
Image
```

**功能：** 图片相册。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### UserGeneric

```cangjie
UserGeneric
```

**功能：** 用户相册。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Video

```cangjie
Video
```

**功能：** 视频相册。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(AlbumSubtype)

```cangjie
public operator func !=(other: AlbumSubtype): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[AlbumSubtype](#enum-albumsubtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(AlbumSubtype)

```cangjie
public operator func ==(other: AlbumSubtype): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[AlbumSubtype](#enum-albumsubtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum AlbumType

```cangjie
public enum AlbumType <: Equatable<AlbumType> & ToString {
    | User
    | System
    | ...
}
```

**功能：** 相册类型，表示是用户相册还是系统预置相册。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- Equatable\<AlbumType>
- ToString

### System

```cangjie
System
```

**功能：** 系统预置相册。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### User

```cangjie
User
```

**功能：** 用户相册。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(AlbumType)

```cangjie
public operator func !=(other: AlbumType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[AlbumType](#enum-albumtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(AlbumType)

```cangjie
public operator func ==(other: AlbumType): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[AlbumType](#enum-albumtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum DefaultChangeUri

```cangjie
public enum DefaultChangeUri <: ToString & Equatable<DefaultChangeUri> {
    | DefaultPhotoUri
    | DefaultAlbumUri
    | ...
}
```

**功能：** DefaultChangeUri子类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- ToString
- Equatable\<DefaultChangeUri>

### DefaultAlbumUri

```cangjie
DefaultAlbumUri
```

**功能：** 默认相册的Uri，与forSubUri{true}一起使用，将接收所有相册的更改通知。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### DefaultPhotoUri

```cangjie
DefaultPhotoUri
```

**功能：** 默认PhotoAsset的Uri，与forSubUri{true}一起使用，将接收所有PhotoAsset的更改通知。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(DefaultChangeUri)

```cangjie
public operator func !=(other: DefaultChangeUri): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[DefaultChangeUri](#enum-defaultchangeuri)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(DefaultChangeUri)

```cangjie
public operator func ==(other: DefaultChangeUri): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[DefaultChangeUri](#enum-defaultchangeuri)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum DeliveryMode

```cangjie
public enum DeliveryMode <: Equatable<DeliveryMode> & ToString {
    | FastMode
    | HighQualityMode
    | BalanceMode
    | ...
}
```

**功能：** 资源分发模式。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- Equatable\<DeliveryMode>
- ToString

### BalanceMode

```cangjie
BalanceMode
```

**功能：** 均衡模式。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### FastMode

```cangjie
FastMode
```

**功能：** 快速模式。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### HighQualityMode

```cangjie
HighQualityMode
```

**功能：** 高质量模式。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(DeliveryMode)

```cangjie
public operator func !=(other: DeliveryMode): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[DeliveryMode](#enum-deliverymode)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(DeliveryMode)

```cangjie
public operator func ==(other: DeliveryMode): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[DeliveryMode](#enum-deliverymode)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum DynamicRangeType

```cangjie
public enum DynamicRangeType <: Equatable<DynamicRangeType> & ToString {
    | Sdr
    | Hdr
    | ...
}
```

**功能：** 媒体文件的动态范围类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- Equatable\<DynamicRangeType>
- ToString

### Hdr

```cangjie
Hdr
```

**功能：** 高动态范围类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Sdr

```cangjie
Sdr
```

**功能：** 标准动态范围类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(DynamicRangeType)

```cangjie
public operator func !=(other: DynamicRangeType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[DynamicRangeType](#enum-dynamicrangetype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(DynamicRangeType)

```cangjie
public operator func ==(other: DynamicRangeType): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[DynamicRangeType](#enum-dynamicrangetype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum MemberType

```cangjie
public enum MemberType {
    | Int64Value(Int64)
    | StringValue(String)
    | BoolValue(Bool)
}
```

**功能：** PhotoAsset的成员类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### BoolValue(Bool)

```cangjie
BoolValue(Bool)
```

**功能：** Bool类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Int64Value(Int64)

```cangjie
Int64Value(Int64)
```

**功能：** Int64类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### StringValue(String)

```cangjie
StringValue(String)
```

**功能：** String类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

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

**功能：** 通知事件的类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- Equatable\<NotifyType>
- ToString

### NotifyAdd

```cangjie
NotifyAdd
```

**功能：** 添加文件集或相册通知的类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### NotifyAlbumAddAsset

```cangjie
NotifyAlbumAddAsset
```

**功能：** 在相册中添加的文件集的通知类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### NotifyAlbumRemoveAsset

```cangjie
NotifyAlbumRemoveAsset
```

**功能：** 在相册中删除的文件集的通知类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### NotifyRemove

```cangjie
NotifyRemove
```

**功能：** 删除文件集或相册的通知类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### NotifyUpdate

```cangjie
NotifyUpdate
```

**功能：** 文件集或相册的更新通知类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(NotifyType)

```cangjie
public operator func !=(other: NotifyType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[NotifyType](#enum-notifytype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(NotifyType)

```cangjie
public operator func ==(other: NotifyType): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[NotifyType](#enum-notifytype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

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

**功能：** 图片和视频文件关键信息。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- ToString
- Equatable\<PhotoKeys>

### BurstKey

```cangjie
BurstKey
```

**功能：** 一组连拍照片的唯一标识：uuid。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### CoverPosition

```cangjie
CoverPosition
```

**功能：** 动态照片的封面位置，具体表示封面帧所对应的视频时间戳（单位：微秒）。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### DateAdded

```cangjie
DateAdded
```

**功能：** 添加日期（添加文件时间距1970年1月1日的秒数值）。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### DateAddedMs

```cangjie
DateAddedMs
```

**功能：** 添加日期（添加文件时间距1970年1月1日的毫秒数值）。

注意：查询照片时，不支持基于该字段排序。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### DateModified

```cangjie
DateModified
```

**功能：** 修改日期（修改文件时间距1970年1月1日的秒数值，修改文件名不会改变此值，当文件内容发生修改时才会更新）。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### DateModifiedMs

```cangjie
DateModifiedMs
```

**功能：** 修改日期（修改文件时间距1970年1月1日的毫秒数值，修改文件名不会改变此值，当文件内容发生修改时才会更新）。

注意：查询照片时，不支持基于该字段排序。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### DateTaken

```cangjie
DateTaken
```

**功能：** 拍摄日期（文件拍照时间距1970年1月1日的秒数值）。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### DisplayName

```cangjie
DisplayName
```

**功能：** 显示名字。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Duration

```cangjie
Duration
```

**功能：** 持续时间（单位：毫秒）。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### DynamicRangeType

```cangjie
DynamicRangeType
```

**功能：** 媒体文件的动态范围类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Favorite

```cangjie
Favorite
```

**功能：** 收藏。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Height

```cangjie
Height
```

**功能：** 图片高度（单位：像素）。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### LcdSize

```cangjie
LcdSize
```

**功能：** LCD图片的宽高，值为width:height拼接而成的字符串。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Orientation

```cangjie
Orientation
```

**功能：** 文件的旋转角度，单位为度。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### PhotoSubtype

```cangjie
PhotoSubtype
```

**功能：** 媒体文件的动态范围类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### PhotoType

```cangjie
PhotoType
```

**功能：** 媒体文件类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Size

```cangjie
Size
```

**功能：** 文件大小（单位：字节）。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### ThmSize

```cangjie
ThmSize
```

**功能：** THUMB图片的宽高，值为width:height拼接而成的字符串。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Title

```cangjie
Title
```

**功能：** 文件标题。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Uri

```cangjie
Uri
```

**功能：** 文件uri。

注意：查询照片时，该字段仅支持使用[DataSharePredicates.equalTo](../ArkData/cj-apis-data_share_predicates.md#func-equaltostring-valuetype)谓词。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Width

```cangjie
Width
```

**功能：** 图片宽度（单位：像素）。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(PhotoKeys)

```cangjie
public operator func !=(other: PhotoKeys): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PhotoKeys](#enum-photokeys)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(PhotoKeys)

```cangjie
public operator func ==(other: PhotoKeys): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PhotoKeys](#enum-photokeys)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum PhotoSubtype

```cangjie
public enum PhotoSubtype <: Equatable<PhotoSubtype> & ToString {
    | Default
    | MovingPhoto
    | Burst
    | ...
}
```

**功能：** 连拍照片文件类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- Equatable\<PhotoSubtype>
- ToString

### Burst

```cangjie
Burst
```

**功能：** 连拍照片文件类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Default

```cangjie
Default
```

**功能：** 默认照片类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### MovingPhoto

```cangjie
MovingPhoto
```

**功能：** 动态照片文件类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(PhotoSubtype)

```cangjie
public operator func !=(other: PhotoSubtype): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PhotoSubtype](#enum-photosubtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(PhotoSubtype)

```cangjie
public operator func ==(other: PhotoSubtype): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PhotoSubtype](#enum-photosubtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum PhotoType

```cangjie
public enum PhotoType <: Equatable<PhotoType> & ToString {
    | Image
    | Video
}
```

**功能：** 媒体文件类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- Equatable\<PhotoType>
- ToString

### Image

```cangjie
Image
```

**功能：** 图片。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### Video

```cangjie
Video
```

**功能：** 视频。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(PhotoType)

```cangjie
public operator func !=(other: PhotoType): Bool 
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PhotoType](#enum-phototype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func ==(PhotoType)

```cangjie
public operator func ==(other: PhotoType): Bool 
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PhotoType](#enum-phototype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String 
```

**功能：** 获取枚举的值。

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

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

**功能：** 可选择的媒体文件类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- Equatable\<PhotoViewMIMETypes>
- ToString

### ImageType

```cangjie
ImageType
```

**功能：** 图片类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### ImageVideoType

```cangjie
ImageVideoType
```

**功能：** 图片和视频类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### MovingPhotoImageType

```cangjie
MovingPhotoImageType
```

**功能：** 动态照片类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### VideoType

```cangjie
VideoType
```

**功能：** 视频类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(PhotoViewMIMETypes)

```cangjie
public operator func !=(other: PhotoViewMIMETypes): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PhotoViewMIMETypes](#enum-photoviewmimetypes)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(PhotoViewMIMETypes)

```cangjie
public operator func ==(other: PhotoViewMIMETypes): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PhotoViewMIMETypes](#enum-photoviewmimetypes)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

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

**功能：** 推荐的图片类型。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- Equatable\<RecommendationType>
- ToString

### BankCard

```cangjie
BankCard
```

**功能：** 银行卡。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### BarCode

```cangjie
BarCode
```

**功能：** 条码。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### DriverLicense

```cangjie
DriverLicense
```

**功能：** 驾驶证。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### DrivingLicense

```cangjie
DrivingLicense
```

**功能：** 行驶证。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### FeaturedSinglePortrait

```cangjie
FeaturedSinglePortrait
```

**功能：** 推荐人像。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### IdCard

```cangjie
IdCard
```

**功能：** 身份证。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### PassPort

```cangjie
PassPort
```

**功能：** 护照。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### ProfilePicture

```cangjie
ProfilePicture
```

**功能：** 头像。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### QrCode

```cangjie
QrCode
```

**功能：** 二维码。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### QrOrBarCode

```cangjie
QrOrBarCode
```

**功能：** 二维码或条码。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(RecommendationType)

```cangjie
public operator func !=(other: RecommendationType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[RecommendationType](#enum-recommendationtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(RecommendationType)

```cangjie
public operator func ==(other: RecommendationType): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[RecommendationType](#enum-recommendationtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum ResourceType

```cangjie
public enum ResourceType <: Equatable<ResourceType> & ToString {
    | ImageResource
    | VideoResource
    | ...
}
```

**功能：** 表示图片资源。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

**父类型：**

- Equatable\<ResourceType>
- ToString

### ImageResource

```cangjie
ImageResource
```

**功能：** 表示图片资源。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### VideoResource

```cangjie
VideoResource
```

**功能：** 表示视频资源。

**系统能力：** SystemCapability.FileManagement.PhotoAccessHelper.Core

**起始版本：** 22

### func !=(ResourceType)

```cangjie
public operator func !=(other: ResourceType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[ResourceType](#enum-resourcetype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(ResourceType)

```cangjie
public operator func ==(other: ResourceType): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[ResourceType](#enum-resourcetype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|
