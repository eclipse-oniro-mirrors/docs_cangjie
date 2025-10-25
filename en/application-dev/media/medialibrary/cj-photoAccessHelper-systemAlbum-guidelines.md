# System Album Resource Usage Guide

photoAccessHelper only provides developers with operations related to favorites, video albums, screenshots, and screen recordings albums.

> **Note:**
>
> In the documentation, where `PhotoAccessHelper` is used, it defaults to using the object obtained during development preparation. If an undefined `PhotoAccessHelper` error occurs due to not adding this code segment, please add it manually.

Unless otherwise specified, the resources to be obtained in the documentation are considered pre-configured and existing in the database. If resources cannot be obtained after executing the sample code, please confirm whether the file has been pre-configured and whether the data exists in the database.

## Favorites

Favorites is a system album. When an image or video is marked as a favorite, it is automatically added to the favorites album. Unmarking it as a favorite removes it from the favorites album.

### Obtaining the Favorites Album Object

Use the [getAlbums](../../../../en/application-dev/reference/MediaLibraryKit/cj-apis-file-photo_access_helper.md#func-getalbumsalbumtype-albumsubtype-fetchoptions) interface to obtain the favorites album object.

**Prerequisites**

- Obtain an instance of the photoAccessHelper module for album management.

**Development Steps**

1. Set the parameters for obtaining the favorites album to `photoAccessHelper.AlbumType.SYSTEM` and `photoAccessHelper.AlbumSubtype.FAVORITE`.
2. Call the `PhotoAccessHelper.getAlbums` interface to obtain the favorites album object.

<!-- compile -->

```cangjie
import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.BusinessException

func example() {
  try {
    let context = ctx.getOrThrow()
    let phAccessHelper = getPhotoAccessHelper(context)
    let fetchResult: AlbumResult = phAccessHelper.getAlbums(AlbumType.SYSTEM, AlbumSubtype.FAVORITE)
    let album: Album = fetchResult.getFirstObject()
    AppLog.info('get favorite album successfully, albumUri: ' + album.albumUri)
    fetchResult.close()
  } catch (e: BusinessException) {
    AppLog.error('get favorite album failed with err: ' + e.toString())
  }
}
```

<!-- compile -->

```cangjie
// main_ability.cj
import ohos.base.AppLog
import ohos.ability.AbilityStage
import ohos.ability.LaunchReason

class MainAbility <: UIAbility {
    public init() {
        super()
        registerSelf()
    }

    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        AppLog.info("MainAbility OnCreated.${want.abilityName}")
        match (launchParam.launchReason) {
            case LaunchReason.START_ABILITY => AppLog.info("START_ABILITY")
            case _ => ()
        }
    }

    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        AppLog.info("MainAbility onWindowStageCreate.")
        windowStage.loadContent("EntryView")
        // declared in index.cj
        ctx = this.context
    }
}
```

### Obtaining Images and Videos from the Favorites Album

First, [obtain the favorites album object](#obtaining-the-favorites-album-object), then call the [getAssets](../../../../en/application-dev/reference/MediaLibraryKit/cj-apis-file-photo_access_helper.md#func-getassetsfetchoptions) interface to obtain resources from the favorites album.

**Prerequisites**

- Obtain an instance of the photoAccessHelper module for album management.

The following example demonstrates obtaining an image from the favorites album.

**Development Steps**

1. [Obtain the favorites album object](#obtaining-the-favorites-album-object).
2. Set up image retrieval conditions to obtain the image.
3. Call the `Album.getAssets` interface to obtain the image resource.
4. Call the [getFirstObject](../../../../en/application-dev/reference/MediaLibraryKit/cj-apis-file-photo_access_helper.md#func-getfirstobject) interface to obtain the first image.

<!-- compile -->

```cangjie
import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.BusinessException

func example() {
    let context = ctx.getOrThrow()
    let phAccessHelper = getPhotoAccessHelper(context)
    let predicates: DataSharePredicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions(
        fetchColumns: [],
        predicates: predicates
    )

  try {
    let albumFetchResult: AlbumResult = phAccessHelper.getAlbums(AlbumType.SYSTEM, AlbumSubtype.FAVORITE)
    let album: Album = albumFetchResult.getFirstObject()
    AppLog.info('get favorite album successfully, albumUri: ' + album.albumUri)

    let photoFetchResult: PhotoAssetResult = album.getAssets(fetchOptions)
    let photoAsset: PhotoAsset = photoFetchResult.getFirstObject()
    AppLog.info('favorite album getAssets successfully, photoAsset displayName: ' + photoAsset.displayName)
    photoFetchResult.close()
    albumFetchResult.close()
  } catch (e: BusinessException) {
    AppLog.error('favorite failed with err: ' + e.toString())
  }
}
```

<!-- compile -->

```cangjie
// main_ability.cj
import ohos.base.AppLog
import ohos.ability.AbilityStage
import ohos.ability.LaunchReason

class MainAbility <: UIAbility {
    public init() {
        super()
        registerSelf()
    }

    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        AppLog.info("MainAbility OnCreated.${want.abilityName}")
        match (launchParam.launchReason) {
            case LaunchReason.START_ABILITY => AppLog.info("START_ABILITY")
            case _ => ()
        }
    }

    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        AppLog.info("MainAbility onWindowStageCreate.")
        windowStage.loadContent("EntryView")
        // declared in index.cj
        ctx = this.context
    }
}
```

## Video Album

The video album is a system album. Media files of the video type in user files are automatically added to the video album.

### Obtaining the Video Album Object

Use the [getAlbums](../../../../en/application-dev/reference/MediaLibraryKit/cj-apis-file-photo_access_helper.md#func-getalbumsalbumtype-albumsubtype-fetchoptions) interface to obtain the video album object.

**Prerequisites**

- Obtain an instance of the photoAccessHelper module for album management.

**Development Steps**

1. Set the parameters for obtaining the video album to `photoAccessHelper.AlbumType.SYSTEM` and `photoAccessHelper.AlbumSubtype.VIDEO`.
2. Call the `PhotoAccessHelper.getAlbums` interface to obtain the video album.

<!-- compile -->

```cangjie
import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.BusinessException

func example() {
  try {
    let context = ctx.getOrThrow()
    let phAccessHelper = getPhotoAccessHelper(context)
    let fetchResult: AlbumResult = phAccessHelper.getAlbums(AlbumType.SYSTEM, AlbumSubtype.VIDEO)
    let album: Album = fetchResult.getFirstObject()
    AppLog.info('get video album successfully, albumUri: ' + album.albumUri)
    fetchResult.close()
  } catch (e: BusinessException) {
    AppLog.error('get video album failed with err: ' + e.toString())
  }
}
```

<!-- compile -->

```cangjie
// main_ability.cj
import ohos.base.AppLog
import ohos.ability.AbilityStage
import ohos.ability.LaunchReason

class MainAbility <: UIAbility {
    public init() {
        super()
        registerSelf()
    }

    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        AppLog.info("MainAbility OnCreated.${want.abilityName}")
        match (launchParam.launchReason) {
            case LaunchReason.START_ABILITY => AppLog.info("START_ABILITY")
            case _ => ()
        }
    }

    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        AppLog.info("MainAbility onWindowStageCreate.")
        windowStage.loadContent("EntryView")
        // declared in index.cj
        ctx = this.context
    }
}
```

### Obtaining Videos from the Video Album

First, [obtain the video album object](#obtaining-the-video-album-object), then call the [getAssets](../../../../en/application-dev/reference/MediaLibraryKit/cj-apis-file-photo_access_helper.md#func-getassetsfetchoptions) interface to obtain video resources from the video album.

**Prerequisites**

- Obtain an instance of the photoAccessHelper module for album management.

The following example demonstrates obtaining a video from the video album.

**Development Steps**

1. First, [obtain the video album object](#obtaining-the-video-album-object).
2. Set up video retrieval conditions to obtain the video.
3. Call the `Album.getAssets` interface to obtain the video resource.
4. Call the [getFirstObject](../../../../en/application-dev/reference/MediaLibraryKit/cj-apis-file-photo_access_helper.md#func-getfirstobject) interface to obtain the first video.

<!-- compile -->

```cangjie
import kit.MediaLibraryKit.*
import kit.ArkData.*
import ohos.base.BusinessException

func example() {
    let context = ctx.getOrThrow()
    let phAccessHelper = getPhotoAccessHelper(context)
    let predicates: DataSharePredicates = DataSharePredicates()
    let fetchOptions: FetchOptions = FetchOptions(
        fetchColumns: [],
        predicates: predicates
    )

  try {
    let albumFetchResult: AlbumResult = phAccessHelper.getAlbums(AlbumType.SYSTEM, AlbumSubtype.VIDEO)
    let album: Album = albumFetchResult.getFirstObject()
    AppLog.info('get video album successfully, albumUri: ' + album.albumUri)

    let videoFetchResult: PhotoAssetResult = album.getAssets(fetchOptions)
    let photoAsset: PhotoAsset = videoFetchResult.getFirstObject()
    AppLog.info('video album getAssets successfully, photoAsset displayName: ' + photoAsset.displayName)
    videoFetchResult.close()
    albumFetchResult.close()
  } catch (e: BusinessException) {
    AppLog.error('video failed with err: ' + e.toString())
  }
}
```

<!-- compile -->

```cangjie
// main_ability.cj
import ohos.base.AppLog
import ohos.ability.AbilityStage
import ohos.ability.LaunchReason

class MainAbility <: UIAbility {
    public init() {
        super()
        registerSelf()
    }

    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        AppLog.info("MainAbility OnCreated.${want.abilityName}")
        match (launchParam.launchReason) {
            case LaunchReason.START_ABILITY => AppLog.info("START_ABILITY")
            case _ => ()
        }
    }

    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        AppLog.info("MainAbility onWindowStageCreate.")
        windowStage.loadContent("EntryView")
        // declared in index.cj
        ctx = this.context
    }
}
```