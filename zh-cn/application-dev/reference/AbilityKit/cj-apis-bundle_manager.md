# ohos.bundle.bundle_manager（bundleManager管理）

提供获取与应用包相关的信息查询能力，包括应用（Application）、模块（HAP Module）、能力（Ability）、扩展能力（ExtensionAbility）、权限、签名等信息。

## 导入模块

```cangjie
import kit.AbilityKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有"// index.cj"注释，表示该示例可在仓颉模板工程的"index.cj"文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的"main_ability.cj"文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## class AbilityInfo

```cangjie
public class AbilityInfo {
    public let bundleName: String
    public let moduleName: String
    public let name: String
    public let label: String
    public let labelId: Int32
    public let description: String
    public let descriptionId: Int32
    public let icon: String
    public let iconId: Int32
    public let process: String
    public let exported: Bool
    public let orientation: DisplayOrientation
    public let launchType: LaunchType
    public let permissions: Array<String>
    public let deviceTypes: Array<String>
    public let applicationInfo: ApplicationInfo
    public let metadata: Array<Metadata>
    public let enabled: Bool
    public let supportWindowModes: Array<SupportWindowMode>
    public let windowSize: WindowSize
    public let excludeFromDock: Bool
    public let skills: Array<Skill>
    public let appIndex: Int32
}
```

**功能：** Ability信息。三方应用可以通过[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)获取Ability信息，其中入参bundleFlags至少包含GET_BUNDLE_INFO_WITH_HAP_MODULE和GET_BUNDLE_INFO_WITH_ABILITY。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let appIndex

```cangjie
public let appIndex: Int32
```

**功能：** 应用包的分身索引标识，仅在分身应用中生效。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let applicationInfo

```cangjie
public let applicationInfo: ApplicationInfo
```

**功能：** 应用程序的配置信息。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_HAP_MODULE、GET_BUNDLE_INFO_WITH_ABILITY和GET_BUNDLE_INFO_WITH_APPLICATION的值。

**类型：** [ApplicationInfo](#class-applicationinfo)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let bundleName

```cangjie
public let bundleName: String
```

**功能：** 应用Bundle名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let description

```cangjie
public let description: String
```

**功能：** Ability的描述。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let descriptionId

```cangjie
public let descriptionId: Int32
```

**功能：** Ability的描述资源id。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let deviceTypes

```cangjie
public let deviceTypes: Array<String>
```

**功能：** Ability支持的设备类型。

**类型：** Array\<String>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let enabled

```cangjie
public let enabled: Bool
```

**功能：** Ability是否可用。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let excludeFromDock

```cangjie
public let excludeFromDock: Bool
```

**功能：** 判断Ability是否可以在dock区域隐藏图标。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let exported

```cangjie
public let exported: Bool
```

**功能：** 判断Ability是否可以被其他应用调用。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let icon

```cangjie
public let icon: String
```

**功能：** Ability的图标资源描述符，如"icon": "$media: icon"。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let iconId

```cangjie
public let iconId: Int32
```

**功能：** Ability的图标资源id。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let label

```cangjie
public let label: String
```

**功能：** Ability对用户显示的名称的资源描述符，如："label": "$string: mainability_description"。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let labelId

```cangjie
public let labelId: Int32
```

**功能：** Ability的标签资源id。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let launchType

```cangjie
public let launchType: LaunchType
```

**功能：** Ability的启动模式。

**类型：** [LaunchType](#enum-launchtype)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let metadata

```cangjie
public let metadata: Array<Metadata>
```

**功能：** Ability的元信息。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_HAP_MODULE、GET_BUNDLE_INFO_WITH_ABILITY和GET_BUNDLE_INFO_WITH_METADATA的值。

**类型：** Array\<[Metadata](./cj-apis-metadata.md#class-metadata)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let moduleName

```cangjie
public let moduleName: String
```

**功能：** Ability所属的HAP的名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let name

```cangjie
public let name: String
```

**功能：** Ability名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let orientation

```cangjie
public let orientation: DisplayOrientation
```

**功能：** Ability的显示模式。

**类型：** [DisplayOrientation](#enum-displayorientation)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let permissions

```cangjie
public let permissions: Array<String>
```

**功能：** 被其他应用Ability调用时需要申请的权限集合。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_HAP_MODULE、GET_BUNDLE_INFO_WITH_ABILITY和GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION的值。

**类型：** Array\<String>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let process

```cangjie
public let process: String
```

**功能：** Ability的进程，如果不设置，默认为包的名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let skills

```cangjie
public let skills: Array<Skill>
```

**功能：** Ability的Skills信息。

**类型：** Array\<[Skill](./cj-apis-skill.md#class-skill)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let supportWindowModes

```cangjie
public let supportWindowModes: Array<SupportWindowMode>
```

**功能：** Ability支持的窗口模式。

**类型：** Array\<[SupportWindowMode](#enum-supportwindowmode)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let windowSize

```cangjie
public let windowSize: WindowSize
```

**功能：** Ability窗口尺寸。

**类型：** [WindowSize](#class-windowsize)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class ApplicationInfo

```cangjie
public class ApplicationInfo {
    public let name: String
    public let description: String
    public let descriptionId: Int32
    public let enabled: Bool
    public let label: String
    public let labelId: Int32
    public let icon: String
    public let iconId: Int32
    public let process: String
    public let permissions: Array<String>
    public let codePath: String
    public let metadataArray: Array<ModuleMetadata>
    public let removable: Bool
    public let accessTokenId: UInt32
    public let uid: Int32
    public let iconResource: AppResource
    public let labelResource: AppResource
    public let descriptionResource: AppResource
    public let appDistributionType: String
    public let appProvisionType: String
    public let systemApp: Bool
    public let bundleType: BundleType
    public let debug: Bool
    public let dataUnclearable: Bool
    public let cloudFileSyncEnabled: Bool
    public let nativeLibraryPath: String
    public let multiAppMode: MultiAppMode
    public let appIndex: Int32
    public let installSource: String
    public let releaseType: String
}
```

**功能：** 应用程序的配置信息。三方应用可以通过[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)获取自身的应用程序信息，其中入参bundleFlags至少包含GET_BUNDLE_INFO_WITH_APPLICATION。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let accessTokenId

```cangjie
public let accessTokenId: UInt32
```

**功能：** 应用程序的accessTokenId。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let appDistributionType

```cangjie
public let appDistributionType: String
```

**功能：** 应用程序签名证书的分发类型，分为：app_gallery、enterprise、os_integration和crowdtesting。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let appIndex

```cangjie
public let appIndex: Int32
```

**功能：** 应用包的分身索引标识，仅在分身应用中生效。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let appProvisionType

```cangjie
public let appProvisionType: String
```

**功能：** 应用程序签名证书文件的类型，分为debug和release两种类型。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let bundleType

```cangjie
public let bundleType: BundleType
```

**功能：** 标识包的类型，取值为APP（应用）或者ATOMIC_SERVICE（元服务）。

**类型：** [BundleType](#enum-bundletype)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let cloudFileSyncEnabled

```cangjie
public let cloudFileSyncEnabled: Bool
```

**功能：** 标识当前应用是否启用端云文件同步能力。true表示当前应用启用端云文件同步能力，false表示当前应用不启用端云文件同步能力。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let codePath

```cangjie
public let codePath: String
```

**功能：** 应用程序的安装目录。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let dataUnclearable

```cangjie
public let dataUnclearable: Bool
```

**功能：** 标识应用数据是否可被删除。true表示不可删除，false表示可以删除。默认为false。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let debug

```cangjie
public let debug: Bool
```

**功能：** 标识应用是否处于调试模式，默认为false。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let description

```cangjie
public let description: String
```

**功能：** 标识应用的描述信息，使用示例："description": $string: mainability_description"。关于description的详细信息可参见descriptionResource字段说明。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let descriptionId

```cangjie
public let descriptionId: Int32
```

**功能：** 标识应用的描述信息的资源id。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let descriptionResource

```cangjie
public let descriptionResource: AppResource
```

**功能：** 应用程序的描述资源信息，包含了bundleName、moduleName和资源的id，可以调用全球化的接口[getMediaContent](../LocalizationKit/cj-apis-resource_manager.md#func-getmediacontentappresource-screendensity)来获取详细的资源数据信息。

**类型：** [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let enabled

```cangjie
public let enabled: Bool
```

**功能：** 判断应用程序是否可以使用，默认为true。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let icon

```cangjie
public let icon: String
```

**功能：** 应用程序的图标，使用示例："icon": "$media: icon"。关于icon的详细信息可参见iconResource字段说明。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let iconId

```cangjie
public let iconId: Int32
```

**功能：** 应用程序图标的资源id。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let iconResource

```cangjie
public let iconResource: AppResource
```

**功能：** 应用程序的图标资源信息，包含了bundleName、moduleName和资源的id，可以调用全球化的接口[getMediaContent](../LocalizationKit/cj-apis-resource_manager.md#func-getmediacontentappresource-screendensity)来获取详细的资源数据信息。

**类型：** [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let installSource

```cangjie
public let installSource: String
```

**功能：** 应用程序的安装来源。pre-installed表示应用为预置应用，格式为包名表示应用由包名对应的应用安装，unknown表示应用安装来源未知。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let label

```cangjie
public let label: String
```

**功能：** 标识应用的名称，使用示例："label": "$string: mainability_description"。关于label的详细信息可参见labelResource字段说明。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let labelId

```cangjie
public let labelId: Int32
```

**功能：** 标识应用名称的资源id。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let labelResource

```cangjie
public let labelResource: AppResource
```

**功能：** 应用程序的标签资源信息，包含了bundleName、moduleName和资源的id，可以调用全球化的接口[getMediaContent](../LocalizationKit/cj-apis-resource_manager.md#func-getmediacontentappresource-screendensity)来获取详细的资源数据信息。

**类型：** [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let metadataArray

```cangjie
public let metadataArray: Array<ModuleMetadata>
```

**功能：** 应用程序的元信息。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_APPLICATION和GET_BUNDLE_INFO_WITH_METADATA的值。

**类型：** Array\<[ModuleMetadata](#class-modulemetadata)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let multiAppMode

```cangjie
public let multiAppMode: MultiAppMode
```

**功能：** 应用多开模式。

**类型：** [MultiAppMode](#class-multiappmode)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let name

```cangjie
public let name: String
```

**功能：** 应用程序的名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let nativeLibraryPath

```cangjie
public let nativeLibraryPath: String
```

**功能：** 应用程序的本地库文件路径。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let permissions

```cangjie
public let permissions: Array<String>
```

**功能：** 访问应用程序所需的权限。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_APPLICATION和GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION的值。

**类型：** Array\<String>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let process

```cangjie
public let process: String
```

**功能：** 应用程序的进程，如果不设置，默认为包的名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let releaseType

```cangjie
public let releaseType: String
```

**功能：** 标识应用打包时使用的SDK的发布类型。当前SDK的发布类型可能为Canary、Beta、Release，其中Canary和Beta可能通过序号进一步细分，例如Canary1、Canary2、Beta1、Beta2等。开发者可通过对比应用打包依赖的SDK发布类型和OS的发布类型（[deviceInfo.distributionOSReleaseType](../BasicServicesKit/cj-apis-device_info.md)）来判断兼容性。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let removable

```cangjie
public let removable: Bool
```

**功能：** 应用程序是否可以被移除。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let systemApp

```cangjie
public let systemApp: Bool
```

**功能：** 标识应用是否为系统应用。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let uid

```cangjie
public let uid: Int32
```

**功能：** 应用程序的uid。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class BundleFlag

```cangjie
public class BundleFlag {
    public static const GET_BUNDLE_INFO_DEFAULT: Int32 = 0x00000000
    public static const GET_BUNDLE_INFO_WITH_APPLICATION: Int32 = 0x00000001
    public static const GET_BUNDLE_INFO_WITH_HAP_MODULE: Int32 = 0x00000002
    public static const GET_BUNDLE_INFO_WITH_ABILITY: Int32 = 0x00000004
    public static const GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY: Int32 = 0x00000008
    public static const GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION: Int32 = 0x00000010
    public static const GET_BUNDLE_INFO_WITH_METADATA: Int32 = 0x00000020
    public static const GET_BUNDLE_INFO_WITH_DISABLE: Int32 = 0x00000040
    public static const GET_BUNDLE_INFO_WITH_SIGNATURE_INFO: Int32 = 0x00000080
    public static const GET_BUNDLE_INFO_WITH_MENU: Int32 = 0x00000100
    public static const GET_BUNDLE_INFO_WITH_ROUTER_MAP: Int32 = 0x00000200
    public static const GET_BUNDLE_INFO_WITH_SKILL: Int32 = 0x00000800
}
```

**功能：** 包信息标志，指示需要获取的包信息的内容。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_DEFAULT

```cangjie
public static const GET_BUNDLE_INFO_DEFAULT: Int32 = 0x00000000
```

**功能：** 只获取最基础的应用包信息。获取到的应用包信息中不包含HAP模块信息、应用信息、签名信息和权限申请信息。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_WITH_ABILITY

```cangjie
public static const GET_BUNDLE_INFO_WITH_ABILITY: Int32 = 0x00000004
```

**功能：** 必须与`GET_BUNDLE_INFO_WITH_HAP_MODULE`同时指定，使得获取到的HAP模块信息中包含能力信息，但不包含能力信息中的元数据。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_WITH_APPLICATION

```cangjie
public static const GET_BUNDLE_INFO_WITH_APPLICATION: Int32 = 0x00000001
```

**功能：** 在最基础的应用包信息的基础上，附带上应用信息，但不包含应用信息中的元数据。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_WITH_DISABLE

```cangjie
public static const GET_BUNDLE_INFO_WITH_DISABLE: Int32 = 0x00000040
```

**功能：** 用于获取application被禁用的BundleInfo和被禁用的Ability信息。获取的bundleInfo不包含signatureInfo、applicationInfo、hapModuleInfo、ability、extensionAbility和permission的信息。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY

```cangjie
public static const GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY: Int32 = 0x00000008
```

**功能：** 必须与`GET_BUNDLE_INFO_WITH_HAP_MODULE`同时指定，使得获取到的HAP模块信息中包含拓展能力信息，但不包含拓展能力信息中的元数据。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_WITH_HAP_MODULE

```cangjie
public static const GET_BUNDLE_INFO_WITH_HAP_MODULE: Int32 = 0x00000002
```

**功能：** 在最基础的应用包信息的基础上，附带上HAP模块信息，但不包含HAP模块信息中的能力信息、拓展能力信息和元数据。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_WITH_MENU

```cangjie
public static const GET_BUNDLE_INFO_WITH_MENU: Int32 = 0x00000100
```

**功能：** 用于获取包含fileContextMenuConfig的bundleInfo。它不能单独使用，需要与GET_BUNDLE_INFO_WITH_HAP_MODULE一起使用。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_WITH_METADATA

```cangjie
public static const GET_BUNDLE_INFO_WITH_METADATA: Int32 = 0x00000020
```

**功能：** 获取所有的元数据，包括HAP模块信息、能力信息、拓展能力信息和应用信息中的元数据，因此必须与`GET_BUNDLE_INFO_WITH_HAP_MODULE`、`GET_BUNDLE_INFO_WITH_ABILITY`、`GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY`和`GET_BUNDLE_INFO_WITH_APPLICATION`同时指定。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION

```cangjie
public static const GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION: Int32 = 0x00000010
```

**功能：** 在最基础的应用包信息的基础上，附带上权限申请信息。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_WITH_ROUTER_MAP

```cangjie
public static const GET_BUNDLE_INFO_WITH_ROUTER_MAP: Int32 = 0x00000200
```

**功能：** 用于获取包含routerMap的bundleInfo。它不能单独使用，需要与GET_BUNDLE_INFO_WITH_HAP_MODULE一起使用。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_WITH_SIGNATURE_INFO

```cangjie
public static const GET_BUNDLE_INFO_WITH_SIGNATURE_INFO: Int32 = 0x00000080
```

**功能：** 用于获取包含signatureInfo的bundleInfo。获取的bundleInfo不包含applicationInfo、hapModuleInfo、extensionAbility、ability和permission的信息。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static const GET_BUNDLE_INFO_WITH_SKILL

```cangjie
public static const GET_BUNDLE_INFO_WITH_SKILL: Int32 = 0x00000800
```

**功能：** 用于获取包含skills的bundleInfo。它不能单独使用，需要与GET_BUNDLE_INFO_WITH_HAP_MODULE、GET_BUNDLE_INFO_WITH_ABILITY、GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY一起使用。

**类型：** Int32

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class BundleInfo

```cangjie
public class BundleInfo {
    public let name: String
    public let vendor: String
    public let versionCode: UInt32
    public let versionName: String
    public let minCompatibleVersionCode: UInt32
    public let targetVersion: UInt32
    public let appInfo: ApplicationInfo
    public let hapModulesInfo: Array<HapModuleInfo>
    public let reqPermissionDetails: Array<ReqPermissionDetail>
    public let permissionGrantStates: Array<PermissionGrantState>
    public let signatureInfo: SignatureInfo
    public let installTime: Int64
    public let updateTime: Int64
    public let routerMap: Array<RouterItem>
    public let appIndex: Int32
}
```

**功能：** 包信息。三方应用可以通过[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)获取自身的应用包信息，其中入参bundleFlags指定所返回的BundleInfo中所包含的信息。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let appIndex

```cangjie
public let appIndex: Int32
```

**功能：** 应用包的分身索引标识，仅在分身应用中生效。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let appInfo

```cangjie
public let appInfo: ApplicationInfo
```

**功能：** 应用程序的配置信息。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_APPLICATION的值。

**类型：** [ApplicationInfo](#class-applicationinfo)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let hapModulesInfo

```cangjie
public let hapModulesInfo: Array<HapModuleInfo>
```

**功能：** 模块的配置信息。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_HAP_MODULE的值。

**类型：** Array\<[HapModuleInfo](#class-hapmoduleinfo)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let installTime

```cangjie
public let installTime: Int64
```

**功能：** 应用包安装时间。

**类型：** Int64

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let minCompatibleVersionCode

```cangjie
public let minCompatibleVersionCode: UInt32
```

**功能：** 分布式场景下的应用包兼容的最低版本。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let name

```cangjie
public let name: String
```

**功能：** 应用包的名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let permissionGrantStates

```cangjie
public let permissionGrantStates: Array<PermissionGrantState>
```

**功能：** 申请权限的授予状态。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION的值。

**类型：** Array\<[PermissionGrantState](#enum-permissiongrantstate)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let reqPermissionDetails

```cangjie
public let reqPermissionDetails: Array<ReqPermissionDetail>
```

**功能：** 应用运行时需向系统申请的权限集合的详细信息。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION的值。

**类型：** Array\<[ReqPermissionDetail](#class-reqpermissiondetail)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let routerMap

```cangjie
public let routerMap: Array<RouterItem>
```

**功能：** 应用的路由表配置，由hapModulesInfo下的routerMap信息，根据RouterItem中的name字段进行去重后合并得到。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_HAP_MODULE和GET_BUNDLE_INFO_WITH_ROUTER_MAP的值。

**类型：** Array\<[RouterItem](#class-routeritem)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let signatureInfo

```cangjie
public let signatureInfo: SignatureInfo
```

**功能：** 应用包的签名信息。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_SIGNATURE_INFO的值。

**类型：** [SignatureInfo](#class-signatureinfo)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let targetVersion

```cangjie
public let targetVersion: UInt32
```

**功能：** 该标签标识应用运行目标版本。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let updateTime

```cangjie
public let updateTime: Int64
```

**功能：** 应用包更新时间。

**类型：** Int64

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let vendor

```cangjie
public let vendor: String
```

**功能：** 应用包的供应商。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let versionCode

```cangjie
public let versionCode: UInt32
```

**功能：** 应用包的版本号。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let versionName

```cangjie
public let versionName: String
```

**功能：** 应用包的版本文本描述信息。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class BundleManager

```cangjie
public class BundleManager {}
```

**功能：** 提供Bundle信息查询方法的类。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### static func canOpenLink(String)

```cangjie
public static func canOpenLink(link: String): Bool
```

**功能：** 查询给定的链接是否可以打开。指定链接的scheme需要在module.json5文件的querySchemes字段下配置。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|link|String|是|-|表示需要查询的链接。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|返回true表示给定的链接可以打开，返回false表示给定的链接不能打开。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[包管理子系统通用错误码](./cj-errorcode-bundle.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 17700055 | The specified link is invalid. |
  | 17700056 | The scheme of the specified link is not in the querySchemes. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

let link = "app1Scheme://test.example.com/home"
let canOpen = BundleManager.canOpenLink(link)
```

### static func getBundleInfoForSelf(Int32)

```cangjie
public static func getBundleInfoForSelf(bundleFlags: Int32): BundleInfo
```

**功能：** 根据给定的bundleFlags获取当前应用的BundleInfo。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|bundleFlags|Int32|是|-|指定返回的BundleInfo所包含的信息，具体可参考[BundleFlag](#class-bundleflag)。|

**返回值：**

|类型|说明|
|:----|:----|
|[BundleInfo](#class-bundleinfo)|BundleInfo对象，返回当前应用的BundleInfo。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.AbilityKit.*

let bundleFlags = GET_BUNDLE_INFO_DEFAULT | GET_BUNDLE_INFO_WITH_APPLICATION | GET_BUNDLE_INFO_WITH_HAP_MODULE | GET_BUNDLE_INFO_WITH_ABILITY
let res = BundleManager.getBundleInfoForSelf(bundleFlags)
```

### static func getProfileByAbility(String, String, String)

```cangjie
public static func getProfileByAbility(moduleName: String, abilityName: String, metadataName!: String = ""): Array<String>
```

**功能：** 根据给定的moduleName、abilityName和metadataName（module.json中metadata标签下的name）获取相应配置文件的json格式字符串，返回对象为String数组。

配置信息资源的资源文件中使用引用定义的资源，在返回的JSON字符串中将保持资源引用的字符串格式，例如`$string: myResourceID`，其中`myResourceID`是工程在构建过程中为资源自动分配的资源ID。开发者可以使用`ohos/resource_manager`包中的相关接口来获取这类引用的资源。

如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如$string: res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

> **说明：**
>
> - 能力的配置信息资源在相应的module.json5文件中`module.abilities[].metadata`标签下定义。
> - 配置信息资源的数据内容是以紧凑的JSON字符串格式返回的。
> - 一个能力可以拥有零到若干个配置信息资源。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|moduleName|String|是|-|目标模块的名称。|
|abilityName|String|是|-|目标能力的名称。|
|metadataName|String|否|""|**命名参数。** 目标配置信息资源的名称。组件的元信息名称，即module.json5配置文件中abilities标签下的metadata标签的name。<br>- 当`metadataName`为目标能力的某配置信息资源的名称时，将只返回该配置信息的数据内容，此时返回的数组中只拥有一个元素。<br>- 当`metadataName`缺省，或为空字符串时，将返回通过模块名称和能力名称确定的能力的所有配置信息的数据内容，此时返回的数组中将拥有零到若干个元素。|

**返回值：**

|类型|说明|
|:----|:----|
|Array\<String>|返回匹配到的配置信息的JSON字符串数组。若指定`metadataName`且存在，仅返回一个元素；未指定或为空时，返回该能力下所有配置信息，可能为空。若配置信息中包含资源引用（如`$string: res_id`），返回值保持引用字符串，需配合资源管理接口解析。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[包管理子系统通用错误码](./cj-errorcode-bundle.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Input parameters check failed. |
  | 17700002 | The specified moduleName is not existed. |
  | 17700003 | The specified abilityName is not existed. |
  | 17700024 | Failed to get the profile because there is no profile in the HAP. |
  | 17700026 | The specified bundle is disabled. |
  | 17700029 | The specified ability is disabled. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.AbilityKit.*

let moduleName = "entry"
let abilityName = "EntryAbility"
let infoList = BundleManager.getProfileByAbility(moduleName, abilityName)
```

### static func getProfileByExtensionAbility(String, String, String)

```cangjie
public static func getProfileByExtensionAbility(moduleName: String, extensionAbilityName: String,
    metadataName!: String = ""): Array<String>
```

**功能：** 根据给定的moduleName、extensionAbilityName和metadataName（module.json中metadata标签下的name）获取相应配置文件的json格式字符串，返回对象为String数组。

配置信息资源的资源文件中使用引用定义的资源，在返回的JSON字符串中将保持资源引用的字符串格式，例如`$string: myResourceID`，其中`myResourceID`是工程在构建过程中为资源自动分配的资源ID。开发者可以使用`ohos/resource_manager`包中的相关接口来获取这类引用的资源。

如果配置文件信息采用了资源引用格式，则返回值将保持资源引用格式（例如$string: res_id），开发者可以通过资源管理模块的相关接口，来获取引用的资源。

> **说明：**
>
> - 拓展能力的配置信息资源在相应的module.json5文件中`module.extensionAbilities[].metadata`标签下定义。
> - 配置信息资源的数据内容以紧凑的JSON字符串格式返回的。
> - 一个拓展能力可以拥有零到若干个配置信息资源。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|moduleName|String|是|-|目标模块的名称。|
|extensionAbilityName|String|是|-|目标拓展能力的名称。|
|metadataName|String|否|""|**命名参数。** 目标配置信息资源的名称。组件的元信息名称，即module.json5配置文件中extensionAbilities标签下的metadata标签的name，默认值为空。<br>- 当`metadataName`为目标拓展能力的某配置信息资源的名称时，将只返回该配置信息的数据内容，此时返回的数组中只拥有一个元素。<br>- 当`metadataName`缺省，或为空字符串时，将返回通过模块名称和拓展能力名称确定的拓展能力的所有配置信息的数据内容，此时返回的数组中将拥有零到若干个元素。|

**返回值：**

|类型|说明|
|:----|:----|
|Array\<String>|返回匹配到的配置信息的JSON字符串数组。若指定`metadataName`且存在，仅返回一个元素；未指定或为空时，返回通过模块名与扩展能力名确定的所有配置信息，可能为空。若配置信息中包含资源引用（如`$string: res_id`），返回值保持引用字符串，需配合资源管理接口解析。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[包管理子系统通用错误码](./cj-errorcode-bundle.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Input parameters check failed. |
  | 17700002 | The specified moduleName is not existed. |
  | 17700003 | The specified extensionAbilityName not existed. |
  | 17700024 | Failed to get the profile because there is no profile in the HAP. |
  | 17700026 | The specified bundle is disabled. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.AbilityKit.*

let moduleName = "entry"
let extensionAbilityName = "EntryFormAbility"
let metadataName = "ohos.extension.form"
let info = BundleManager.getProfileByExtensionAbility(moduleName, extensionAbilityName, metadataName: metadataName)
```

## class DataItem

```cangjie
public class DataItem {
    public let key: String
    public let value: String
}
```

**功能：** 描述模块配置的路由表中的自定义数据。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let key

```cangjie
public let key: String
```

**功能：** 标识路由表自定义数据的键。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let value

```cangjie
public let value: String
```

**功能：** 标识路由表自定义数据的值。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class DefaultAppManager

```cangjie
public class DefaultAppManager {}
```

**功能：** 该类提供查询默认应用的能力，支持查询当前应用是否是默认应用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

### static func isDefaultApplication(String)

```cangjie
public static func isDefaultApplication(appType: String): Bool
```

**功能：** 根据系统已定义的应用类型，判断当前应用是否是该类型的默认应用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|appType|String|是|-|要查询的应用类型，取[ApplicationType](#enum-applicationtype)中的值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|返回当前应用是否是默认应用，true表示是默认应用，false表示不是默认应用。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[包管理子系统通用错误码](./cj-errorcode-bundle.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 801 | Capability not supported. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.AbilityKit.*

let tag = DefaultAppManager.isDefaultApplication(ApplicationType.Image.getValue())
```

## class Dependency

```cangjie
public class Dependency {
    public let bundleName: String
    public let moduleName: String
    public let versionCode: UInt32
}
```

**功能：** 描述模块所依赖的动态共享库信息。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let bundleName

```cangjie
public let bundleName: String
```

**功能：** 标识当前模块依赖的共享包包名。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let moduleName

```cangjie
public let moduleName: String
```

**功能：** 标识当前模块依赖的共享包模块名。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let versionCode

```cangjie
public let versionCode: UInt32
```

**功能：** 标识当前共享包的版本号。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class ExtensionAbilityInfo

```cangjie
public class ExtensionAbilityInfo {
    public let bundleName: String
    public let moduleName: String
    public let name: String
    public let labelId: Int32
    public let descriptionId: Int32
    public let iconId: Int32
    public let exported: Bool
    public let extensionAbilityType: ExtensionAbilityType
    public let permissions: Array<String>
    public let applicationInfo: ApplicationInfo
    public let metadata: Array<Metadata>
    public let enabled: Bool
    public let readPermission: String
    public let writePermission: String
    public let extensionAbilityTypeName: String
    public let skills: Array<Skill>
    public let appIndex: Int32
}
```

**功能：** ExtensionAbilityInfo信息。三方应用可以通过[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)获取自身的ExtensionAbility信息，其中入参bundleFlags至少包含GET_BUNDLE_INFO_WITH_HAP_MODULE和GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let appIndex

```cangjie
public let appIndex: Int32
```

**功能：** 应用包的分身索引标识，仅在分身应用中生效。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let applicationInfo

```cangjie
public let applicationInfo: ApplicationInfo
```

**功能：** 应用程序的配置信息。

**类型：** [ApplicationInfo](#class-applicationinfo)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let bundleName

```cangjie
public let bundleName: String
```

**功能：** 应用Bundle名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let descriptionId

```cangjie
public let descriptionId: Int32
```

**功能：** ExtensionAbility的描述资源ID。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let enabled

```cangjie
public let enabled: Bool
```

**功能：** ExtensionAbility是否可用。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let exported

```cangjie
public let exported: Bool
```

**功能：** 判断ExtensionAbility是否可以被其他应用调用。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let extensionAbilityType

```cangjie
public let extensionAbilityType: ExtensionAbilityType
```

**功能：** ExtensionAbility类型。

**类型：** [ExtensionAbilityType](#enum-extensionabilitytype)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let extensionAbilityTypeName

```cangjie
public let extensionAbilityTypeName: String
```

**功能：** ExtensionAbility的类型名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let iconId

```cangjie
public let iconId: Int32
```

**功能：** ExtensionAbility的图标资源ID。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let labelId

```cangjie
public let labelId: Int32
```

**功能：** ExtensionAbility的标签资源ID。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let metadata

```cangjie
public let metadata: Array<Metadata>
```

**功能：** ExtensionAbility的元信息。

**类型：** Array\<[Metadata](./cj-apis-metadata.md#class-metadata)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let moduleName

```cangjie
public let moduleName: String
```

**功能：** ExtensionAbility所属的HAP的名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let name

```cangjie
public let name: String
```

**功能：** ExtensionAbility名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let permissions

```cangjie
public let permissions: Array<String>
```

**功能：** 被其他应用ExtensionAbility调用时需要申请的权限集合。

**类型：** Array\<String>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let readPermission

```cangjie
public let readPermission: String
```

**功能：** 读取ExtensionAbility数据所需的权限。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let skills

```cangjie
public let skills: Array<Skill>
```

**功能：** ExtensionAbility的Skills信息。

**类型：** Array\<[Skill](./cj-apis-skill.md#class-skill)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let writePermission

```cangjie
public let writePermission: String
```

**功能：** 向ExtensionAbility写数据所需的权限。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class HapModuleInfo

```cangjie
public class HapModuleInfo {
    public let name: String
    public let icon: String
    public let iconId: Int32
    public let label: String
    public let labelId: Int32
    public let description: String
    public let descriptionId: Int32
    public let mainElementName: String
    public let abilitiesInfo: Array<AbilityInfo>
    public let extensionAbilitiesInfo: Array<ExtensionAbilityInfo>
    public let metadata: Array<Metadata>
    public let deviceTypes: Array<String>
    public let installationFree: Bool
    public let hashValue: String
    public let moduleType: ModuleType
    public let preloads: Array<PreloadItem>
    public let dependencies: Array<Dependency>
    public let fileContextMenuConfig: String
    public let routerMap: Array<RouterItem>
    public let codePath: String
    public let nativeLibraryPath: String
}
```

**功能：** HAP信息。三方应用可以通过[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)获取自身的HAP信息，其中入参bundleFlags至少包含GET_BUNDLE_INFO_WITH_HAP_MODULE。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let abilitiesInfo

```cangjie
public let abilitiesInfo: Array<AbilityInfo>
```

**功能：** Ability信息。

**类型：** Array\<[AbilityInfo](#class-abilityinfo)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let codePath

```cangjie
public let codePath: String
```

**功能：** 模块的安装路径。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let dependencies

```cangjie
public let dependencies: Array<Dependency>
```

**功能：** 模块运行依赖的动态共享库列表。

**类型：** Array\<[Dependency](#class-dependency)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let description

```cangjie
public let description: String
```

**功能：** 模块描述信息。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let descriptionId

```cangjie
public let descriptionId: Int32
```

**功能：** 描述信息的资源id值。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let deviceTypes

```cangjie
public let deviceTypes: Array<String>
```

**功能：** 可以运行模块的设备类型。

**类型：** Array\<String>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let extensionAbilitiesInfo

```cangjie
public let extensionAbilitiesInfo: Array<ExtensionAbilityInfo>
```

**功能：** ExtensionAbility信息。

**类型：** Array\<[ExtensionAbilityInfo](#class-extensionabilityinfo)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let fileContextMenuConfig

```cangjie
public let fileContextMenuConfig: String
```

**功能：** 模块的文件菜单配置。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let hashValue

```cangjie
public let hashValue: String
```

**功能：** 模块的Hash值。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let icon

```cangjie
public let icon: String
```

**功能：** 模块图标。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let iconId

```cangjie
public let iconId: Int32
```

**功能：** 模块图标的资源id值。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let installationFree

```cangjie
public let installationFree: Bool
```

**功能：** 模块是否支持免安装。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let label

```cangjie
public let label: String
```

**功能：** 模块标签。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let labelId

```cangjie
public let labelId: Int32
```

**功能：** 模块标签的资源id值。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let mainElementName

```cangjie
public let mainElementName: String
```

**功能：** 入口ability信息。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let metadata

```cangjie
public let metadata: Array<Metadata>
```

**功能：** Ability的元信息。

**类型：** Array\<[Metadata](./cj-apis-metadata.md#class-metadata)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let moduleType

```cangjie
public let moduleType: ModuleType
```

**功能：** 标识当前模块的类型。

**类型：** [ModuleType](#enum-moduletype)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let name

```cangjie
public let name: String
```

**功能：** 模块名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let nativeLibraryPath

```cangjie
public let nativeLibraryPath: String
```

**功能：** 应用程序内某个hapModule的本地库文件路径。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let preloads

```cangjie
public let preloads: Array<PreloadItem>
```

**功能：** 元服务中模块的预加载列表。

**类型：** Array\<[PreloadItem](#class-preloaditem)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let routerMap

```cangjie
public let routerMap: Array<RouterItem>
```

**功能：** 模块的路由表配置。通过调用[getBundleInfoForSelf](#static-func-getbundleinfoforselfint32)接口获取，bundleFlags参数传入GET_BUNDLE_INFO_WITH_HAP_MODULE和GET_BUNDLE_INFO_WITH_ROUTER_MAP的值。

**类型：** Array\<[RouterItem](#class-routeritem)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class ModuleMetadata

```cangjie
public class ModuleMetadata {
    public let moduleName: String
    public let metadata: Array<Metadata>
}
```

**功能：** 描述模块的元数据信息。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let metadata

```cangjie
public let metadata: Array<Metadata>
```

**功能：** 该模块下的元数据信息列表。

**类型：** Array\<[Metadata](./cj-apis-metadata.md#class-metadata)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let moduleName

```cangjie
public let moduleName: String
```

**功能：** 模块名。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class MultiAppMode

```cangjie
public class MultiAppMode {
    public let multiAppModeType: MultiAppModeType
    public let maxCount: Int32
}
```

**功能：** 表示应用多开模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let maxCount

```cangjie
public let maxCount: Int32
```

**功能：** 表示应用在当前多开模式下允许的最大实例（分身/多实例）数量。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let multiAppModeType

```cangjie
public let multiAppModeType: MultiAppModeType
```

**功能：** 应用多开模式的类型。

**类型：** [MultiAppModeType](#enum-multiappmodetype)

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class PreloadItem

```cangjie
public class PreloadItem {
    public let moduleName: String
}
```

**功能：** 描述元服务中模块的预加载模块信息。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let moduleName

```cangjie
public let moduleName: String
```

**功能：** 模块运行时，由系统自动执行预加载的模块名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class ReqPermissionDetail

```cangjie
public class ReqPermissionDetail {
    public var name: String
    public var moduleName: String
    public var reason: String
    public var reasonId: Int32
    public var usedScene: UsedScene
}
```

**功能：** 应用运行时需向系统申请的权限集合的详细信息。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### var moduleName

```cangjie
public var moduleName: String
```

**功能：** 申请该权限的module名称。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### var name

```cangjie
public var name: String
```

**功能：** 需要使用的权限名称。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### var reason

```cangjie
public var reason: String
```

**功能：** 描述申请权限的原因。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### var reasonId

```cangjie
public var reasonId: Int32
```

**功能：** 描述申请权限的原因ID。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### var usedScene

```cangjie
public var usedScene: UsedScene
```

**功能：** 权限使用的场景和时机。

**类型：** [UsedScene](#class-usedscene)

**读写能力：** 可读写

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class RouterItem

```cangjie
public class RouterItem {
    public let name: String
    public let pageSourceFile: String
    public let buildFunction: String
    public let data: Array<DataItem>
    public let customData: String
}
```

**功能：** 描述模块配置的路由表信息。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let buildFunction

```cangjie
public let buildFunction: String
```

**功能：** 标识被@Builder修饰的函数，该函数描述页面的UI。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let customData

```cangjie
public let customData: String
```

**功能：** 标识路由表配置文件中的任意类型的自定义数据。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let data

```cangjie
public let data: Array<DataItem>
```

**功能：** 标识路由表配置文件中的字符串自定义数据，即data字段的信息，该字段已由系统解析，无需开发者自行解析。

**类型：** Array\<[DataItem](#class-dataitem)>

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let name

```cangjie
public let name: String
```

**功能：** 标识跳转页面的名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let pageSourceFile

```cangjie
public let pageSourceFile: String
```

**功能：** 标识页面在模块内的路径。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class SignatureInfo

```cangjie
public class SignatureInfo {
    public let appId: String
    public let fingerprint: String
    public let appIdentifier: String
}
```

**功能：** 描述应用包的签名信息。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let appId

```cangjie
public let appId: String
```

**功能：** 应用的appId。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let appIdentifier

```cangjie
public let appIdentifier: String
```

**功能：** 应用的唯一标识，由云端统一分配。该ID在应用全生命周期中不会发生变化，包括版本升级、证书变更、开发者公私钥变更、应用转移等。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let fingerprint

```cangjie
public let fingerprint: String
```

**功能：** 应用包的指纹信息。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class UsedScene

```cangjie
public class UsedScene {
    public var abilities: Array<String>
    public var when: String
}
```

**功能：** 描述权限使用的场景和时机。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### var abilities

```cangjie
public var abilities: Array<String>
```

**功能：** 使用到该权限的Ability集合。

**类型：** Array\<String>

**读写能力：** 可读写

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### var when

```cangjie
public var when: String
```

**功能：** 使用该权限的时机。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## class WindowSize

```cangjie
public class WindowSize {
    public let maxWindowRatio: Float64
    public let minWindowRatio: Float64
    public let maxWindowWidth: UInt32
    public let minWindowWidth: UInt32
    public let maxWindowHeight: UInt32
    public let minWindowHeight: UInt32
}
```

**功能：** 描述窗口尺寸。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let maxWindowHeight

```cangjie
public let maxWindowHeight: UInt32
```

**功能：** 表示自由窗口状态下窗口的最大高度，宽度单位为vp。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let maxWindowRatio

```cangjie
public let maxWindowRatio: Float64
```

**功能：** 表示自由窗口状态下窗口的最大宽高比，取值范围0-1。

**类型：** Float64

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let maxWindowWidth

```cangjie
public let maxWindowWidth: UInt32
```

**功能：** 表示自由窗口状态下窗口的最大宽度，宽度单位为vp。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let minWindowHeight

```cangjie
public let minWindowHeight: UInt32
```

**功能：** 表示自由窗口状态下窗口的最小高度，宽度单位为vp。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let minWindowRatio

```cangjie
public let minWindowRatio: Float64
```

**功能：** 表示自由窗口状态下窗口的最小宽高比，取值范围0-1。

**类型：** Float64

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### let minWindowWidth

```cangjie
public let minWindowWidth: UInt32
```

**功能：** 表示自由窗口状态下窗口的最小宽度，宽度单位为vp。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## enum ApplicationType

```cangjie
public enum ApplicationType {
    | Browser
    | Image
    | Audio
    | Video
    | Pdf
    | Word
    | Excel
    | Ppt
    | Email
    | ...
}
```

**功能：** 默认应用的应用类型。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

### Audio

```cangjie
Audio
```

**功能：** 默认音频播放器。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

### Browser

```cangjie
Browser
```

**功能：** 默认浏览器。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

### Email

```cangjie
Email
```

**功能：** 默认邮件。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

### Excel

```cangjie
Excel
```

**功能：** 默认EXCEL文档查看器。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

### Image

```cangjie
Image
```

**功能：** 默认图片查看器。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

### Pdf

```cangjie
Pdf
```

**功能：** 默认PDF文档查看器。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

### Ppt

```cangjie
Ppt
```

**功能：** 默认PPT文档查看器。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

### Video

```cangjie
Video
```

**功能：** 默认视频播放器。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

### Word

```cangjie
Word
```

**功能：** 默认WORD文档查看器。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

### func getValue()

```cangjie
public func getValue(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.BundleManager.BundleFramework.DefaultApp

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的值。|

## enum BundleType

```cangjie
public enum BundleType {
    | App
    | AtomicService
    | ...
}
```

**功能：** 标识应用的类型。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### App

```cangjie
App
```

**功能：** 该Bundle是应用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### AtomicService

```cangjie
AtomicService
```

**功能：** 该Bundle是元服务。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## enum DisplayOrientation

```cangjie
public enum DisplayOrientation {
    | Unspecified
    | Landscape
    | Portrait
    | FollowRecent
    | LandscapeInverted
    | PortraitInverted
    | AutoRotation
    | AutoRotationLandscape
    | AutoRotationPortrait
    | AutoRotationRestricted
    | AutoRotationLandscapeRestricted
    | AutoRotationPortraitRestricted
    | Locked
    | AutoRotationUnspecified
    | FollowDesktop
    | ...
}
```

**功能：** 标识该Ability的显示模式。该标签仅适用于page类型的Ability。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### AutoRotation

```cangjie
AutoRotation
```

**功能：** 表示传感器自动旋转模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### AutoRotationLandscape

```cangjie
AutoRotationLandscape
```

**功能：** 表示传感器自动横向旋转模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### AutoRotationLandscapeRestricted

```cangjie
AutoRotationLandscapeRestricted
```

**功能：** 表示受开关控制的自动横向旋转模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### AutoRotationPortrait

```cangjie
AutoRotationPortrait
```

**功能：** 表示传感器自动竖向旋转模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### AutoRotationPortraitRestricted

```cangjie
AutoRotationPortraitRestricted
```

**功能：** 表示受开关控制的自动竖向旋转模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### AutoRotationRestricted

```cangjie
AutoRotationRestricted
```

**功能：** 表示受开关控制的自动旋转模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### AutoRotationUnspecified

```cangjie
AutoRotationUnspecified
```

**功能：** 受开关控制和由系统判定的自动旋转模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### FollowDesktop

```cangjie
FollowDesktop
```

**功能：** 跟随桌面的旋转模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### FollowRecent

```cangjie
FollowRecent
```

**功能：** 表示跟随上一个显示模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Landscape

```cangjie
Landscape
```

**功能：** 表示横屏显示模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### LandscapeInverted

```cangjie
LandscapeInverted
```

**功能：** 表示反向横屏显示模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Locked

```cangjie
Locked
```

**功能：** 表示锁定模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Portrait

```cangjie
Portrait
```

**功能：** 表示竖屏显示模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### PortraitInverted

```cangjie
PortraitInverted
```

**功能：** 表示反向竖屏显示模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Unspecified

```cangjie
Unspecified
```

**功能：** 表示未定义方向模式，由系统判定。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## enum ExtensionAbilityType

```cangjie
public enum ExtensionAbilityType {
    | Form
    | WorkScheduler
    | InputMethod
    | Service
    | Accessibility
    | DataShare
    | FileShare
    | StaticSubscriber
    | Wallpaper
    | Backup
    | Window
    | EnterpriseAdmin
    | Thumbnail
    | Preview
    | Print
    | Share
    | Push
    | Driver
    | Action
    | AdsService
    | EmbeddedUi
    | InsightIntentUi
    | Unspecified
    | ...
}
```

**功能：** 指示扩展组件的类型。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Accessibility

```cangjie
Accessibility
```

**功能：** 无障碍服务扩展能力，支持访问与操作前台界面。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Action

```cangjie
Action
```

**功能：** 自定义服务扩展能力，为开发者提供基于UIExtension的自定义操作业务模板。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### AdsService

```cangjie
AdsService
```

**功能：** 广告服务扩展能力，对外提供后台自定义广告业务服务，当前暂未支持。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Backup

```cangjie
Backup
```

**功能：** 数据备份扩展能力，提供应用数据的备份恢复能力。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### DataShare

```cangjie
DataShare
```

**功能：** 数据共享扩展能力，用于对外提供数据读写服务。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Driver

```cangjie
Driver
```

**功能：** 驱动扩展能力，提供外设驱动扩展能力，当前暂未支持。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### EmbeddedUi

```cangjie
EmbeddedUi
```

**功能：** 嵌入式UI扩展能力，提供跨进程界面嵌入的能力。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### EnterpriseAdmin

```cangjie
EnterpriseAdmin
```

**功能：** 企业设备管理扩展能力，提供企业管理时处理管理事件的能力，比如设备上应用安装事件、锁屏密码输入错误次数过多事件等。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### FileShare

```cangjie
FileShare
```

**功能：** 文件共享扩展能力，用于应用间的文件分享。预留能力，当前暂未支持。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Form

```cangjie
Form
```

**功能：** 卡片扩展能力，提供卡片开发能力。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### InputMethod

```cangjie
InputMethod
```

**功能：** 输入法扩展能力，用于开发输入法应用。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### InsightIntentUi

```cangjie
InsightIntentUi
```

**功能：** 为开发者提供能被小艺意图调用，以窗口形态呈现内容的扩展能力。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Preview

```cangjie
Preview
```

**功能：** 文件预览扩展能力，提供文件预览的能力，其他应用可以直接在应用中嵌入显示。预留能力，当前暂未支持。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Print

```cangjie
Print
```

**功能：** 文件打印扩展能力，提供应用打印照片、文档等办公场景。当前支持图片打印，文档类型暂未支持。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Push

```cangjie
Push
```

**功能：** 推送扩展能力，提供推送场景化消息能力。预留能力，当前暂未支持。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Service

```cangjie
Service
```

**功能：** 后台服务扩展能力，提供后台运行并对外提供相应能力。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Share

```cangjie
Share
```

**功能：** 提供分享业务能力，为开发者提供基于UIExtension的分享业务模板。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### StaticSubscriber

```cangjie
StaticSubscriber
```

**功能：** 静态广播扩展能力，用于处理静态事件，比如开机事件。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Thumbnail

```cangjie
Thumbnail
```

**功能：** 文件缩略图扩展能力，用于为文件提供图标缩略图的能力。预留能力，当前暂未支持。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Unspecified

```cangjie
Unspecified
```

**功能：** 不指定类型，配合queryExtensionAbilityInfo接口可以查询所有类型的ExtensionAbility。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Wallpaper

```cangjie
Wallpaper
```

**功能：** 壁纸扩展能力，用于实现桌面壁纸。预留能力，当前暂未支持。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Window

```cangjie
Window
```

**功能：** 界面组合扩展能力，允许系统应用进行跨应用的界面拉起和嵌入。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### WorkScheduler

```cangjie
WorkScheduler
```

**功能：** 延时任务扩展能力，允许应用在系统闲时执行实时性不高的任务。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## enum LaunchType

```cangjie
public enum LaunchType {
    | Singleton
    | Multiton
    | Specified
    | ...
}
```

**功能：** 一个能力拥有一种启动类型，该枚举用于标明该能力的启动类型。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Multiton

```cangjie
Multiton
```

**功能：** 能力以普通多实例的方式启动。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Singleton

```cangjie
Singleton
```

**功能：** 能力以单实例的方式启动。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Specified

```cangjie
Specified
```

**功能：** 能力以自定义多实例的方式启动。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## enum ModuleType

```cangjie
public enum ModuleType {
    | Entry
    | Feature
    | Shared
    | ...
}
```

**功能：** 标识模块类型。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Entry

```cangjie
Entry
```

**功能：** 应用的主模块。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Feature

```cangjie
Feature
```

**功能：** 应用的动态特性模块。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Shared

```cangjie
Shared
```

**功能：** 应用的动态共享库模块。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## enum MultiAppModeType

```cangjie
public enum MultiAppModeType {
    | Unspecified
    | MultiInstance
    | AppClone
    | ...
}
```

**功能：** 标识应用多开的模式类型。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### AppClone

```cangjie
AppClone
```

**功能：** 分身模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### MultiInstance

```cangjie
MultiInstance
```

**功能：** 多实例模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Unspecified

```cangjie
Unspecified
```

**功能：** 未指定类型。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## enum PermissionGrantState

```cangjie
public enum PermissionGrantState {
    | PermissionDenied
    | PermissionGranted
    | ...
}
```

**功能：** 指示权限授予状态。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### PermissionDenied

```cangjie
PermissionDenied
```

**功能：** 拒绝授予权限。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### PermissionGranted

```cangjie
PermissionGranted
```

**功能：** 授予权限。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

## enum SupportWindowMode

```cangjie
public enum SupportWindowMode {
    | FullScreen
    | Split
    | Floating
    | ...
}
```

**功能：** 一个能力（Ability）可以支持若干个窗口模式，该枚举用于标明某个能力所支持的窗口模式。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Floating

```cangjie
Floating
```

**功能：** 支持窗口化显示。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### FullScreen

```cangjie
FullScreen
```

**功能：** 窗口支持全屏显示。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22

### Split

```cangjie
Split
```

**功能：** 窗口支持分屏显示。

**系统能力：** SystemCapability.BundleManager.BundleFramework.Core

**起始版本：** 22
