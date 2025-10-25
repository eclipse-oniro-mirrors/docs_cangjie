# ohos.bundle.bundle_manager (BundleManager Management)

Provides capabilities for querying information related to application packages, including applications (Application), modules (HAP Module), abilities (Ability), extension abilities (ExtensionAbility), permissions, signatures, and other information.

## Import Module

```cangjie
import kit.AbilityKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the aforementioned sample project and configuration template, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-sample-code-instructions).

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

**Function:** Ability information. Third-party applications can obtain Ability information through [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32), where the input parameter bundleFlags must include at least GET_BUNDLE_INFO_WITH_HAP_MODULE and GET_BUNDLE_INFO_WITH_ABILITY.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let appIndex

```cangjie
public let appIndex: Int32
```

**Function:** The clone index identifier of the application package, effective only in clone applications.

**Type:** Int32

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let applicationInfo

```cangjie
public let applicationInfo: ApplicationInfo
```

**Function:** Configuration information of the application. Obtained by calling the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter passing the values of GET_BUNDLE_INFO_WITH_HAP_MODULE, GET_BUNDLE_INFO_WITH_ABILITY, and GET_BUNDLE_INFO_WITH_APPLICATION.

**Type:** [ApplicationInfo](#class-applicationinfo)

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let bundleName

```cangjie
public let bundleName: String
```

**Function:** The bundle name of the application.

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let description

```cangjie
public let description: String
```

**Function:** Description of the Ability.

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let descriptionId

```cangjie
public let descriptionId: Int32
```

**Function:** Resource ID of the Ability's description.

**Type:** Int32

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let deviceTypes

```cangjie
public let deviceTypes: Array<String>
```

**Function:** Device types supported by the Ability.

**Type:** Array\<String>

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let enabled

```cangjie
public let enabled: Bool
```

**Function:** Whether the Ability is enabled.

**Type:** Bool

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let excludeFromDock

```cangjie
public let excludeFromDock: Bool
```

**Function:** Determines whether the Ability can hide its icon in the dock area.

**Type:** Bool

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let exported

```cangjie
public let exported: Bool
```

**Function:** Determines whether the Ability can be called by other applications.

**Type:** Bool

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let icon

```cangjie
public let icon: String
```

**Function:** Icon resource descriptor of the Ability, such as "icon": "$media: icon".

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let iconId

```cangjie
public let iconId: Int32
```

**Function:** Resource ID of the Ability's icon.

**Type:** Int32

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let label

```cangjie
public let label: String
```

**Function:** Resource descriptor of the name displayed to users for the Ability, such as: "label": "$string: mainability_description".

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let labelId

```cangjie
public let labelId: Int32
```

**Function:** Resource ID of the Ability's label.

**Type:** Int32

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let launchType

```cangjie
public let launchType: LaunchType
```

**Function:** Launch mode of the Ability.

**Type:** [LaunchType](#enum-launchtype)

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let metadata

```cangjie
public let metadata: Array<Metadata>
```

**Function:** Metadata of the Ability. Obtained by calling the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter passing the values of GET_BUNDLE_INFO_WITH_HAP_MODULE, GET_BUNDLE_INFO_WITH_ABILITY, and GET_BUNDLE_INFO_WITH_METADATA.

**Type:** Array\<[Metadata](./cj-apis-metadata.md#class-metadata)>

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let moduleName

```cangjie
public let moduleName: String
```

**Function:** Name of the HAP to which the Ability belongs.

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let name

```cangjie
public let name: String
```

**Function:** Name of the Ability.

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let orientation

```cangjie
public let orientation: DisplayOrientation
```

**Function:** Display mode of the Ability.

**Type:** [DisplayOrientation](#enum-displayorientation)

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let permissions

```cangjie
public let permissions: Array<String>
```

**Function:** Set of permissions required when calling the Ability from other applications. Obtained by calling the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter passing the values of GET_BUNDLE_INFO_WITH_HAP_MODULE, GET_BUNDLE_INFO_WITH_ABILITY, and GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION.

**Type:** Array\<String>

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let process

```cangjie
public let process: String
```

**Function:** Process of the Ability. If not set, it defaults to the package name.

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let skills

```cangjie
public let skills: Array<Skill>
```

**Function:** Skills information of the Ability.

**Type:** Array\<[Skill](./cj-apis-skill.md#class-skill)>

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let supportWindowModes

```cangjie
public let supportWindowModes: Array<SupportWindowMode>
```

**Function:** Window modes supported by the Ability.

**Type:** Array\<[SupportWindowMode](#enum-supportwindowmode)>

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let windowSize

```cangjie
public let windowSize: WindowSize
```

**Function:** Window size of the Ability.

**Type:** [WindowSize](#class-windowsize)

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21## class ApplicationInfo

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

**Function:** Configuration information of the application. Third-party applications can obtain their own application information through [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32), where the input parameter bundleFlags must include at least GET_BUNDLE_INFO_WITH_APPLICATION.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let accessTokenId

```cangjie
public let accessTokenId: UInt32
```

**Function:** The accessTokenId of the application.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let appDistributionType

```cangjie
public let appDistributionType: String
```

**Function:** The distribution type of the application's signing certificate, which can be: app_gallery, enterprise, os_integration, or crowdtesting.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let appIndex

```cangjie
public let appIndex: Int32
```

**Function:** The clone index identifier of the application package, effective only in clone applications.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let appProvisionType

```cangjie
public let appProvisionType: String
```

**Function:** The type of the application's signing certificate file, which can be debug or release.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let bundleType

```cangjie
public let bundleType: BundleType
```

**Function:** Identifies the type of the package, which can be APP (application) or ATOMIC_SERVICE (atomic service).

**Type:** [BundleType](#enum-bundletype)

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let cloudFileSyncEnabled

```cangjie
public let cloudFileSyncEnabled: Bool
```

**Function:** Indicates whether the current application has cloud file synchronization capability enabled. true means the current application has cloud file synchronization capability enabled, false means it does not.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let codePath

```cangjie
public let codePath: String
```

**Function:** The installation directory of the application.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let dataUnclearable

```cangjie
public let dataUnclearable: Bool
```

**Function:** Indicates whether the application data can be deleted. true means it cannot be deleted, false means it can. Default is false.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let debug

```cangjie
public let debug: Bool
```

**Function:** Indicates whether the application is in debug mode. Default is false.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let description

```cangjie
public let description: String
```

**Function:** The description information of the application, example usage: "description": "$string: mainability_description". For detailed information about description, refer to the descriptionResource field.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let descriptionId

```cangjie
public let descriptionId: Int32
```

**Function:** The resource ID of the application's description information.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let descriptionResource

```cangjie
public let descriptionResource: AppResource
```

**Function:** The description resource information of the application, including bundleName, moduleName, and resource ID. The detailed resource data can be obtained by calling the globalization interface [getMediaContent](../LocalizationKit/cj-apis-resource_manager.md#func-getmediacontentappresource-screendensity).

**Type:** [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource)

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let enabled

```cangjie
public let enabled: Bool
```

**Function:** Determines whether the application can be used. Default is true.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let icon

```cangjie
public let icon: String
```

**Function:** The icon of the application, example usage: "icon": "$media: icon". For detailed information about icon, refer to the iconResource field.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let iconId

```cangjie
public let iconId: Int32
```

**Function:** The resource ID of the application's icon.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let iconResource

```cangjie
public let iconResource: AppResource
```

**Function:** The icon resource information of the application, including bundleName, moduleName, and resource ID. The detailed resource data can be obtained by calling the globalization interface [getMediaContent](../LocalizationKit/cj-apis-resource_manager.md#func-getmediacontentappresource-screendensity).

**Type:** [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource)

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let installSource

```cangjie
public let installSource: String
```

**Function:** The installation source of the application. pre-installed means the application is pre-installed, the format is the package name indicating the application was installed by the corresponding application, unknown means the installation source is unknown.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let label

```cangjie
public let label: String
```

**Function:** The name of the application, example usage: "label": "$string: mainability_description". For detailed information about label, refer to the labelResource field.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let labelId

```cangjie
public let labelId: Int32
```

**Function:** The resource ID of the application's name.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let labelResource

```cangjie
public let labelResource: AppResource
```

**Function:** The label resource information of the application, including bundleName, moduleName, and resource ID. The detailed resource data can be obtained by calling the globalization interface [getMediaContent](../LocalizationKit/cj-apis-resource_manager.md#func-getmediacontentappresource-screendensity).

**Type:** [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource)

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let metadataArray

```cangjie
public let metadataArray: Array<ModuleMetadata>
```

**Function:** The metadata of the application. Obtained by calling the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter set to the values of GET_BUNDLE_INFO_WITH_APPLICATION and GET_BUNDLE_INFO_WITH_METADATA.

**Type:** Array\<[ModuleMetadata](#class-modulemetadata)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let multiAppMode

```cangjie
public let multiAppMode: MultiAppMode
```

**Function:** The multi-instance mode of the application.

**Type:** [MultiAppMode](#class-multiappmode)

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let name

```cangjie
public let name: String
```

**Function:** The name of the application.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let nativeLibraryPath

```cangjie
public let nativeLibraryPath: String
```

**Function:** The path to the native library files of the application.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let permissions

```cangjie
public let permissions: Array<String>
```

**Function:** The permissions required to access the application. Obtained by calling the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter set to the values of GET_BUNDLE_INFO_WITH_APPLICATION and GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION.

**Type:** Array\<String>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let process

```cangjie
public let process: String
```

**Function:** The process of the application. If not set, defaults to the package name.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let releaseType

```cangjie
public let releaseType: String
```

**Function:** Identifies the release type of the SDK used when packaging the application. Current SDK release types may include Canary, Beta, Release, where Canary and Beta may be further subdivided by sequence numbers, such as Canary1, Canary2, Beta1, Beta2, etc. Developers can compare the SDK release type the application depends on with the OS release type ([deviceInfo.distributionOSReleaseType](../BasicServicesKit/cj-apis-device_info.md)) to determine compatibility.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let removable

```cangjie
public let removable: Bool
```

**Function:** Whether the application can be removed.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let systemApp

```cangjie
public let systemApp: Bool
```

**Function:** Indicates whether the application is a system application.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let uid

```cangjie
public let uid: Int32
```

**Function:** The uid of the application.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21## class BundleFlag

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

**Description:** Bundle information flags indicating the content of bundle information to be retrieved.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_DEFAULT

```cangjie
public static const GET_BUNDLE_INFO_DEFAULT: Int32 = 0x00000000
```

**Description:** Retrieves only the most basic application bundle information. The obtained bundle information does not include HAP module information, application information, signature information, or permission request information.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_WITH_ABILITY

```cangjie
public static const GET_BUNDLE_INFO_WITH_ABILITY: Int32 = 0x00000004
```

**Description:** Must be specified together with `GET_BUNDLE_INFO_WITH_HAP_MODULE` to include ability information in the retrieved HAP module information, excluding metadata in the ability information.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_WITH_APPLICATION

```cangjie
public static const GET_BUNDLE_INFO_WITH_APPLICATION: Int32 = 0x00000001
```

**Description:** On top of the basic application bundle information, includes application information, excluding metadata in the application information.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_WITH_DISABLE

```cangjie
public static const GET_BUNDLE_INFO_WITH_DISABLE: Int32 = 0x00000040
```

**Description:** Used to retrieve BundleInfo where the application is disabled and disabled Ability information. The retrieved bundleInfo does not include signatureInfo, applicationInfo, hapModuleInfo, ability, extensionAbility, or permission information.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY

```cangjie
public static const GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY: Int32 = 0x00000008
```

**Description:** Must be specified together with `GET_BUNDLE_INFO_WITH_HAP_MODULE` to include extension ability information in the retrieved HAP module information, excluding metadata in the extension ability information.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_WITH_HAP_MODULE

```cangjie
public static const GET_BUNDLE_INFO_WITH_HAP_MODULE: Int32 = 0x00000002
```

**Description:** On top of the basic application bundle information, includes HAP module information, excluding ability information, extension ability information, and metadata in the HAP module information.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_WITH_MENU

```cangjie
public static const GET_BUNDLE_INFO_WITH_MENU: Int32 = 0x00000100
```

**Description:** Used to retrieve bundleInfo containing fileContextMenuConfig. It cannot be used alone and must be used together with GET_BUNDLE_INFO_WITH_HAP_MODULE.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_WITH_METADATA

```cangjie
public static const GET_BUNDLE_INFO_WITH_METADATA: Int32 = 0x00000020
```

**Description:** Retrieves all metadata, including metadata in HAP module information, ability information, extension ability information, and application information. Therefore, it must be specified together with `GET_BUNDLE_INFO_WITH_HAP_MODULE`, `GET_BUNDLE_INFO_WITH_ABILITY`, `GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY`, and `GET_BUNDLE_INFO_WITH_APPLICATION`.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION

```cangjie
public static const GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION: Int32 = 0x00000010
```

**Description:** On top of the basic application bundle information, includes permission request information.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_WITH_ROUTER_MAP

```cangjie
public static const GET_BUNDLE_INFO_WITH_ROUTER_MAP: Int32 = 0x00000200
```

**Description:** Used to retrieve bundleInfo containing routerMap. It cannot be used alone and must be used together with GET_BUNDLE_INFO_WITH_HAP_MODULE.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_WITH_SIGNATURE_INFO

```cangjie
public static const GET_BUNDLE_INFO_WITH_SIGNATURE_INFO: Int32 = 0x00000080
```

**Description:** Used to retrieve bundleInfo containing signatureInfo. The retrieved bundleInfo does not include applicationInfo, hapModuleInfo, extensionAbility, ability, or permission information.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static const GET_BUNDLE_INFO_WITH_SKILL

```cangjie
public static const GET_BUNDLE_INFO_WITH_SKILL: Int32 = 0x00000800
```

**Description:** Used to retrieve bundleInfo containing skills. It cannot be used alone and must be used together with GET_BUNDLE_INFO_WITH_HAP_MODULE, GET_BUNDLE_INFO_WITH_ABILITY, and GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY.

**Type:** Int32

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

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

**Description:** Bundle information. Third-party applications can retrieve their own bundle information via [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32), where the bundleFlags parameter specifies the information to be included in the returned BundleInfo.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let appIndex

```cangjie
public let appIndex: Int32
```

**Description:** The clone index identifier of the application bundle, effective only in clone applications.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let appInfo

```cangjie
public let appInfo: ApplicationInfo
```

**Description:** Configuration information of the application. Retrieved via the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter set to GET_BUNDLE_INFO_WITH_APPLICATION.

**Type:** [ApplicationInfo](#class-applicationinfo)

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let hapModulesInfo

```cangjie
public let hapModulesInfo: Array<HapModuleInfo>
```

**Description:** Configuration information of the modules. Retrieved via the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter set to GET_BUNDLE_INFO_WITH_HAP_MODULE.

**Type:** Array\<[HapModuleInfo](#class-hapmoduleinfo)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let installTime

```cangjie
public let installTime: Int64
```

**Description:** Installation time of the application bundle.

**Type:** Int64

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let minCompatibleVersionCode

```cangjie
public let minCompatibleVersionCode: UInt32
```

**Description:** Minimum compatible version of the application bundle in distributed scenarios.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let name

```cangjie
public let name: String
```

**Description:** Name of the application bundle.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let permissionGrantStates

```cangjie
public let permissionGrantStates: Array<PermissionGrantState>
```

**Description:** Grant states of requested permissions. Retrieved via the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter set to GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION.

**Type:** Array\<[PermissionGrantState](#enum-permissiongrantstate)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let reqPermissionDetails

```cangjie
public let reqPermissionDetails: Array<ReqPermissionDetail>
```

**Description:** Detailed information of the permission set that the application needs to request from the system during runtime. Retrieved via the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter set to GET_BUNDLE_INFO_WITH_REQUESTED_PERMISSION.

**Type:** Array\<[ReqPermissionDetail](#class-reqpermissiondetail)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let routerMap

```cangjie
public let routerMap: Array<RouterItem>
```

**Description:** Router table configuration of the application, obtained by deduplicating and merging routerMap information under hapModulesInfo based on the name field in RouterItem. Retrieved via the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter set to GET_BUNDLE_INFO_WITH_HAP_MODULE and GET_BUNDLE_INFO_WITH_ROUTER_MAP.

**Type:** Array\<[RouterItem](#class-routeritem)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let signatureInfo

```cangjie
public let signatureInfo: SignatureInfo
```

**Description:** Signature information of the application bundle. Retrieved via the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with the bundleFlags parameter set to GET_BUNDLE_INFO_WITH_SIGNATURE_INFO.

**Type:** [SignatureInfo](#class-signatureinfo)

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let targetVersion

```cangjie
public let targetVersion: UInt32
```

**Description:** This tag identifies the target version for the application to run.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let updateTime

```cangjie
public let updateTime: Int64
```

**Description:** Update time of the application bundle.

**Type:** Int64

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let vendor

```cangjie
public let vendor: String
```

**Description:** Vendor of the application bundle.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let versionCode

```cangjie
public let versionCode: UInt32
```

**Description:** Version code of the application bundle.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let versionName

```cangjie
public let versionName: String
```

**Description:** Version description text of the application bundle.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21## class BundleManager

```cangjie
public class BundleManager {}
```

**Description:** A class that provides methods for querying bundle information.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### static func canOpenLink(String)

```cangjie
public static func canOpenLink(link: String): Bool
```

**Description:** Queries whether a given link can be opened. The scheme of the specified link must be configured in the `querySchemes` field of the module.json5 file.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| link | String | Yes | - | The link to be queried. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the given link can be opened; otherwise, returns `false`. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bundle Management Subsystem Common Error Codes](./cj-errorcode-bundle.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 17700055 | The specified link is invalid. |
  | 17700056 | The scheme of the specified link is not in the querySchemes. |

**Example:**

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

**Description:** Obtains the BundleInfo of the current application based on the given bundleFlags.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| bundleFlags | Int32 | Yes | - | Specifies the information to be included in the returned BundleInfo. For details, see [BundleFlag](#class-bundleflag). |

**Return Value:**

| Type | Description |
|:----|:----|
| [BundleInfo](#class-bundleinfo) | A BundleInfo object containing the BundleInfo of the current application. |

**Example:**

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

**Description:** Obtains the JSON-formatted string of the corresponding configuration file based on the given moduleName, abilityName, and metadataName (the name under the metadata tag in module.json). The returned object is an array of strings.

If the configuration information resource uses referenced resources in the resource file, the returned JSON string will maintain the resource reference string format, such as `$string: myResourceID`, where `myResourceID` is the resource ID automatically assigned to the resource during the project build process. Developers can use the relevant interfaces in the `ohos/resource_manager` package to obtain such referenced resources.

If the configuration file information uses the resource reference format, the return value will maintain the resource reference format (e.g., `$string: res_id`). Developers can use the relevant interfaces of the resource management module to obtain the referenced resources.

> **Note:**
>
> - The configuration information resources of the ability are defined under the `module.abilities[].metadata` tag in the corresponding module.json5 file.
> - The data content of the configuration information resources is returned in a compact JSON string format.
> - An ability can have zero to multiple configuration information resources.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| moduleName | String | Yes | - | The name of the target module. |
| abilityName | String | Yes | - | The name of the target ability. |
| metadataName | String | No | "" | **Named parameter.** The name of the target configuration information resource. The metadata name of the component, which is the name under the metadata tag in the abilities tag of the module.json5 configuration file.<br>- When `metadataName` is the name of a configuration information resource of the target ability, only the data content of that configuration information will be returned, and the returned array will contain only one element.<br>- When `metadataName` is omitted or is an empty string, all configuration information data content of the ability determined by the module name and ability name will be returned, and the returned array will contain zero to multiple elements. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | Returns an array of JSON strings of the matched configuration information. If `metadataName` is specified and exists, only one element is returned; if not specified or empty, all configuration information of the ability is returned, which may be empty. If the configuration information contains resource references (e.g., `$string: res_id`), the return value maintains the reference string, which needs to be resolved using the resource management interfaces. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bundle Management Subsystem Common Error Codes](./cj-errorcode-bundle.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Input parameters check failed. |
  | 17700002 | The specified moduleName is not existed. |
  | 17700003 | The specified abilityName is not existed. |
  | 17700024 | Failed to get the profile because there is no profile in the HAP. |
  | 17700026 | The specified bundle is disabled. |
  | 17700029 | The specified ability is disabled. |

**Example:**

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

**Description:** Obtains the JSON-formatted string of the corresponding configuration file based on the given moduleName, extensionAbilityName, and metadataName (the name under the metadata tag in module.json). The returned object is an array of strings.

If the configuration information resource uses referenced resources in the resource file, the returned JSON string will maintain the resource reference string format, such as `$string: myResourceID`, where `myResourceID` is the resource ID automatically assigned to the resource during the project build process. Developers can use the relevant interfaces in the `ohos/resource_manager` package to obtain such referenced resources.

If the configuration file information uses the resource reference format, the return value will maintain the resource reference format (e.g., `$string: res_id`). Developers can use the relevant interfaces of the resource management module to obtain the referenced resources.

> **Note:**
>
> - The configuration information resources of the extension ability are defined under the `module.extensionAbilities[].metadata` tag in the corresponding module.json5 file.
> - The data content of the configuration information resources is returned in a compact JSON string format.
> - An extension ability can have zero to multiple configuration information resources.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| moduleName | String | Yes | - | The name of the target module. |
| extensionAbilityName | String | Yes | - | The name of the target extension ability. |
| metadataName | String | No | "" | **Named parameter.** The name of the target configuration information resource. The metadata name of the component, which is the name under the metadata tag in the extensionAbilities tag of the module.json5 configuration file. The default value is empty.<br>- When `metadataName` is the name of a configuration information resource of the target extension ability, only the data content of that configuration information will be returned, and the returned array will contain only one element.<br>- When `metadataName` is omitted or is an empty string, all configuration information data content of the extension ability determined by the module name and extension ability name will be returned, and the returned array will contain zero to multiple elements. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | Returns an array of JSON strings of the matched configuration information. If `metadataName` is specified and exists, only one element is returned; if not specified or empty, all configuration information determined by the module name and extension ability name is returned, which may be empty. If the configuration information contains resource references (e.g., `$string: res_id`), the return value maintains the reference string, which needs to be resolved using the resource management interfaces. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bundle Management Subsystem Common Error Codes](./cj-errorcode-bundle.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Input parameters check failed. |
  | 17700002 | The specified moduleName is not existed. |
  | 17700003 | The specified extensionAbilityName not existed. |
  | 17700024 | Failed to get the profile because there is no profile in the HAP. |
  | 17700026 | The specified bundle is disabled. |

**Example:**

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

**Description:** Describes custom data in the routing table of a module configuration.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let key

```cangjie
public let key: String
```

**Description:** The key of the custom data in the routing table.

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let value

```cangjie
public let value: String
```

**Description:** The value of the custom data in the routing table.

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

## class DefaultAppManager

```cangjie
public class DefaultAppManager {}
```

**Description:** This class provides the capability to query default applications, supporting queries to determine whether the current application is the default application.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

### static func isDefaultApplication(String)

```cangjie
public static func isDefaultApplication(appType: String): Bool
```

**Description:** Determines whether the current application is the default application of the specified type based on the system-defined application types.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| appType | String | Yes | - | The application type to query, which is a value from [ApplicationType](#enum-applicationtype). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns whether the current application is the default application. `true` indicates it is the default application; `false` indicates it is not. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bundle Management Subsystem Common Error Codes](./cj-errorcode-bundle.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 801 | Capability not supported. |

**Example:**

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

**Description:** Describes the dynamic shared library information that a module depends on.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let bundleName

```cangjie
public let bundleName: String
```

**Description:** The bundle name of the shared library that the current module depends on.

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let moduleName

```cangjie
public let moduleName: String
```

**Description:** The module name of the shared library that the current module depends on.

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let versionCode

```cangjie
public let versionCode: UInt32
```

**Description:** The version code of the current shared library.

**Type:** UInt32

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

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

**Description:** ExtensionAbilityInfo information. Third-party applications can obtain their own ExtensionAbility information through [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32), where the input parameter bundleFlags must include at least GET_BUNDLE_INFO_WITH_HAP_MODULE and GET_BUNDLE_INFO_WITH_EXTENSION_ABILITY.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let appIndex

```cangjie
public let appIndex: Int32
```

**Description:** The clone index identifier of the application package, which takes effect only in clone applications.

**Type:** Int32

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let applicationInfo

```cangjie
public let applicationInfo: ApplicationInfo
```

**Description:** The configuration information of the application.

**Type:** [ApplicationInfo](#class-applicationinfo)

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let bundleName

```cangjie
public let bundleName: String
```

**Description:** The bundle name of the application.

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let descriptionId

```cangjie
public let descriptionId: Int32
```

**Description:** The resource ID of the description of the ExtensionAbility.

**Type:** Int32

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let enabled

```cangjie
public let enabled: Bool
```

**Description:** Whether the ExtensionAbility is enabled.

**Type:** Bool

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let exported

```cangjie
public let exported: Bool
```

**Description:** Determines whether the ExtensionAbility can be called by other applications.

**Type:** Bool

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let extensionAbilityType

```cangjie
public let extensionAbilityType: ExtensionAbilityType
```

**Description:** The type of the ExtensionAbility.

**Type:** [ExtensionAbilityType](#enum-extensionabilitytype)

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let extensionAbilityTypeName

```cangjie
public let extensionAbilityTypeName: String
```

**Description:** The type name of the ExtensionAbility.

**Type:** String

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let iconId

```cangjie
public let iconId: Int32
```

**Description:** The resource ID of the icon of the ExtensionAbility.

**Type:** Int32

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let labelId

```cangjie
public let labelId: Int32
```

**Description:** The resource ID of the label of## class HapModuleInfo

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

**Description:** HAP information. Third-party applications can obtain their own HAP information via [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32), where the input parameter bundleFlags must include at least GET_BUNDLE_INFO_WITH_HAP_MODULE.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let abilitiesInfo

```cangjie
public let abilitiesInfo: Array<AbilityInfo>
```

**Description:** Ability information.

**Type:** Array\<[AbilityInfo](#class-abilityinfo)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let codePath

```cangjie
public let codePath: String
```

**Description:** Installation path of the module.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let dependencies

```cangjie
public let dependencies: Array<Dependency>
```

**Description:** List of dynamically shared libraries that the module depends on for operation.

**Type:** Array\<[Dependency](#class-dependency)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let description

```cangjie
public let description: String
```

**Description:** Module description information.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let descriptionId

```cangjie
public let descriptionId: Int32
```

**Description:** Resource ID value of the description information.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let deviceTypes

```cangjie
public let deviceTypes: Array<String>
```

**Description:** Device types capable of running the module.

**Type:** Array\<String>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let extensionAbilitiesInfo

```cangjie
public let extensionAbilitiesInfo: Array<ExtensionAbilityInfo>
```

**Description:** ExtensionAbility information.

**Type:** Array\<[ExtensionAbilityInfo](#class-extensionabilityinfo)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let fileContextMenuConfig

```cangjie
public let fileContextMenuConfig: String
```

**Description:** File context menu configuration of the module.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let hashValue

```cangjie
public let hashValue: String
```

**Description:** Hash value of the module.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let icon

```cangjie
public let icon: String
```

**Description:** Module icon.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let iconId

```cangjie
public let iconId: Int32
```

**Description:** Resource ID value of the module icon.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let installationFree

```cangjie
public let installationFree: Bool
```

**Description:** Whether the module supports installation-free.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let label

```cangjie
public let label: String
```

**Description:** Module label.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let labelId

```cangjie
public let labelId: Int32
```

**Description:** Resource ID value of the module label.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let mainElementName

```cangjie
public let mainElementName: String
```

**Description:** Entry ability information.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let metadata

```cangjie
public let metadata: Array<Metadata>
```

**Description:** Metadata information of the Ability.

**Type:** Array\<[Metadata](./cj-apis-metadata.md#class-metadata)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let moduleType

```cangjie
public let moduleType: ModuleType
```

**Description:** Identifies the type of the current module.

**Type:** [ModuleType](#enum-moduletype)

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let name

```cangjie
public let name: String
```

**Description:** Module name.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let nativeLibraryPath

```cangjie
public let nativeLibraryPath: String
```

**Description:** Path to the native library files of a hapModule within the application.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let preloads

```cangjie
public let preloads: Array<PreloadItem>
```

**Description:** Preload list of modules in the meta service.

**Type:** Array\<[PreloadItem](#class-preloaditem)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let routerMap

```cangjie
public let routerMap: Array<RouterItem>
```

**Description:** Router table configuration of the module. Obtained by calling the [getBundleInfoForSelf](#static-func-getbundleinfoforselfint32) interface, with bundleFlags parameter passing the values of GET_BUNDLE_INFO_WITH_HAP_MODULE and GET_BUNDLE_INFO_WITH_ROUTER_MAP.

**Type:** Array\<[RouterItem](#class-routeritem)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

## class ModuleMetadata

```cangjie
public class ModuleMetadata {
    public let moduleName: String
    public let metadata: Array<Metadata>
}
```

**Description:** Describes the metadata information of a module.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let metadata

```cangjie
public let metadata: Array<Metadata>
```

**Description:** List of metadata information under this module.

**Type:** Array\<[Metadata](./cj-apis-metadata.md#class-metadata)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let moduleName

```cangjie
public let moduleName: String
```

**Description:** Module name.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21## class MultiAppMode

```cangjie
public class MultiAppMode {
    public let multiAppModeType: MultiAppModeType
    public let maxCount: Int32
}
```

**Description:** Represents the multi-instance mode of an application.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let maxCount

```cangjie
public let maxCount: Int32
```

**Description:** Indicates the maximum number of instances (clones/multi-instances) allowed for the application in the current multi-instance mode.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let multiAppModeType

```cangjie
public let multiAppModeType: MultiAppModeType
```

**Description:** The type of multi-instance mode for the application.

**Type:** [MultiAppModeType](#enum-multiappmodetype)

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

## class PreloadItem

```cangjie
public class PreloadItem {
    public let moduleName: String
}
```

**Description:** Describes the preload module information in a meta-service module.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let moduleName

```cangjie
public let moduleName: String
```

**Description:** The name of the module that will be automatically preloaded by the system during module runtime.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

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

**Description:** Detailed information about the set of permissions that an application needs to request from the system during runtime.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### var moduleName

```cangjie
public var moduleName: String
```

**Description:** The name of the module requesting the permission.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### var name

```cangjie
public var name: String
```

**Description:** The name of the permission to be used.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### var reason

```cangjie
public var reason: String
```

**Description:** Describes the reason for requesting the permission.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### var reasonId

```cangjie
public var reasonId: Int32
```

**Description:** The ID of the reason for requesting the permission.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### var usedScene

```cangjie
public var usedScene: UsedScene
```

**Description:** The scenarios and timing for using the permission.

**Type:** [UsedScene](#class-usedscene)

**Access:** Read-write

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

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

**Description:** Describes the routing table information configured in a module.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let buildFunction

```cangjie
public let buildFunction: String
```

**Description:** Identifies the function decorated with @Builder, which describes the UI of the page.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let customData

```cangjie
public let customData: String
```

**Description:** Identifies custom data of any type in the routing table configuration file.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let data

```cangjie
public let data: Array<DataItem>
```

**Description:** Identifies string-type custom data in the routing table configuration file, i.e., the information in the data field, which has been parsed by the system and does not require manual parsing by developers.

**Type:** Array\<[DataItem](#class-dataitem)>

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let name

```cangjie
public let name: String
```

**Description:** Identifies the name of the page to navigate to.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let pageSourceFile

```cangjie
public let pageSourceFile: String
```

**Description:** Identifies the path of the page within the module.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

## class SignatureInfo

```cangjie
public class SignatureInfo {
    public let appId: String
    public let fingerprint: String
    public let appIdentifier: String
}
```

**Description:** Describes the signature information of an application package.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let appId

```cangjie
public let appId: String
```

**Description:** The appId of the application.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let appIdentifier

```cangjie
public let appIdentifier: String
```

**Description:** The unique identifier of the application, uniformly assigned by the cloud. This ID remains unchanged throughout the application's lifecycle, including version upgrades, certificate changes, developer key pair changes, and application transfers.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let fingerprint

```cangjie
public let fingerprint: String
```

**Description:** The fingerprint information of the application package.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

## class UsedScene

```cangjie
public class UsedScene {
    public var abilities: Array<String>
    public var when: String
}
```

**Description:** Describes the scenarios and timing for using a permission.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### var abilities

```cangjie
public var abilities: Array<String>
```

**Description:** The collection of Abilities that use this permission.

**Type:** Array\<String>

**Access:** Read-write

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### var when

```cangjie
public var when: String
```

**Description:** The timing for using this permission.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

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

**Description:** Describes the window dimensions.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let maxWindowHeight

```cangjie
public let maxWindowHeight: UInt32
```

**Description:** Indicates the maximum height of the window in free-window state, with the width unit in vp.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let maxWindowRatio

```cangjie
public let maxWindowRatio: Float64
```

**Description:** Indicates the maximum aspect ratio of the window in free-window state, with a value range of 0-1.

**Type:** Float64

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let maxWindowWidth

```cangjie
public let maxWindowWidth: UInt32
```

**Description:** Indicates the maximum width of the window in free-window state, with the width unit in vp.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let minWindowHeight

```cangjie
public let minWindowHeight: UInt32
```

**Description:** Indicates the minimum height of the window in free-window state, with the width unit in vp.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let minWindowRatio

```cangjie
public let minWindowRatio: Float64
```

**Description:** Indicates the minimum aspect ratio of the window in free-window state, with a value range of 0-1.

**Type:** Float64

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### let minWindowWidth

```cangjie
public let minWindowWidth: UInt32
```

**Description:** Indicates the minimum width of the window in free-window state, with the width unit in vp.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21## enum ApplicationType

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

**Description:** Application types for default applications.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

### Audio

```cangjie
Audio
```

**Description:** Default audio player.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

### Browser

```cangjie
Browser
```

**Description:** Default browser.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

### Email

```cangjie
Email
```

**Description:** Default email application.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

### Excel

```cangjie
Excel
```

**Description:** Default EXCEL document viewer.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

### Image

```cangjie
Image
```

**Description:** Default image viewer.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

### Pdf

```cangjie
Pdf
```

**Description:** Default PDF document viewer.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

### Ppt

```cangjie
Ppt
```

**Description:** Default PPT document viewer.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

### Video

```cangjie
Video
```

**Description:** Default video player.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

### Word

```cangjie
Word
```

**Description:** Default WORD document viewer.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

### func getValue()

```cangjie
public func getValue(): String
```

**Description:** Gets the enumeration value.

**System Capability:** SystemCapability.BundleManager.BundleFramework.DefaultApp

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|String|The enumeration value.|

## enum BundleType

```cangjie
public enum BundleType {
    | App
    | AtomicService
    | ...
}
```

**Description:** Identifies the type of application.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### App

```cangjie
App
```

**Description:** The bundle is an application.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### AtomicService

```cangjie
AtomicService
```

**Description:** The bundle is an atomic service.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

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

**Description:** Identifies the display mode of the Ability. This tag is only applicable to page-type Abilities.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### AutoRotation

```cangjie
AutoRotation
```

**Description:** Indicates sensor-based auto-rotation mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### AutoRotationLandscape

```cangjie
AutoRotationLandscape
```

**Description:** Indicates sensor-based auto-landscape rotation mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### AutoRotationLandscapeRestricted

```cangjie
AutoRotationLandscapeRestricted
```

**Description:** Indicates switch-controlled auto-landscape rotation mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### AutoRotationPortrait

```cangjie
AutoRotationPortrait
```

**Description:** Indicates sensor-based auto-portrait rotation mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### AutoRotationPortraitRestricted

```cangjie
AutoRotationPortraitRestricted
```

**Description:** Indicates switch-controlled auto-portrait rotation mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### AutoRotationRestricted

```cangjie
AutoRotationRestricted
```

**Description:** Indicates switch-controlled auto-rotation mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### AutoRotationUnspecified

```cangjie
AutoRotationUnspecified
```

**Description:** Indicates switch-controlled and system-determined auto-rotation mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### FollowDesktop

```cangjie
FollowDesktop
```

**Description:** Follows desktop rotation mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### FollowRecent

```cangjie
FollowRecent
```

**Description:** Follows the previous display mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Landscape

```cangjie
Landscape
```

**Description:** Indicates landscape display mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### LandscapeInverted

```cangjie
LandscapeInverted
```

**Description:** Indicates inverted landscape display mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Locked

```cangjie
Locked
```

**Description:** Indicates locked mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Portrait

```cangjie
Portrait
```

**Description:** Indicates portrait display mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### PortraitInverted

```cangjie
PortraitInverted
```

**Description:** Indicates inverted portrait display mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Unspecified

```cangjie
Unspecified
```

**Description:** Indicates undefined orientation mode, determined by the system.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

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

**Description:** Indicates the type of extension ability.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21### Accessibility

```cangjie
Accessibility
```

**Function:** Accessibility service extension capability, supporting access and operation of foreground interfaces.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Action

```cangjie
Action
```

**Function:** Custom service extension capability, providing developers with a UIExtension-based custom operation business template.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### AdsService

```cangjie
AdsService
```

**Function:** Advertising service extension capability, offering background custom advertising business services (currently unsupported).

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Backup

```cangjie
Backup
```

**Function:** Data backup extension capability, providing application data backup and recovery functionality.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### DataShare

```cangjie
DataShare
```

**Function:** Data sharing extension capability, enabling external data read/write services.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Driver

```cangjie
Driver
```

**Function:** Driver extension capability, providing peripheral driver extension functionality (currently unsupported).

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### EmbeddedUi

```cangjie
EmbeddedUi
```

**Function:** Embedded UI extension capability, enabling cross-process interface embedding.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### EnterpriseAdmin

```cangjie
EnterpriseAdmin
```

**Function:** Enterprise device management extension capability, handling management events such as application installation events or excessive incorrect lock screen password attempts.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### FileShare

```cangjie
FileShare
```

**Function:** File sharing extension capability for inter-application file sharing (reserved capability, currently unsupported).

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Form

```cangjie
Form
```

**Function:** Card extension capability, providing card development functionality.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### InputMethod

```cangjie
InputMethod
```

**Function:** Input method extension capability for developing input method applications.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### InsightIntentUi

```cangjie
InsightIntentUi
```

**Function:** Provides developers with extension capability to present content in window form when invoked by Xiaoyi's intent.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Preview

```cangjie
Preview
```

**Function:** File preview extension capability, enabling embedded file preview display in other applications (reserved capability, currently unsupported).

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Print

```cangjie
Print
```

**Function:** File printing extension capability for office scenarios like photo/document printing (currently supports image printing only).

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Push

```cangjie
Push
```

**Function:** Push notification extension capability for contextual message delivery (reserved capability, currently unsupported).

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Service

```cangjie
Service
```

**Function:** Background service extension capability, running in background and providing corresponding functionalities.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Share

```cangjie
Share
```

**Function:** Sharing business capability, providing developers with a UIExtension-based sharing business template.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### StaticSubscriber

```cangjie
StaticSubscriber
```

**Function:** Static broadcast extension capability for handling static events like boot events.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Thumbnail

```cangjie
Thumbnail
```

**Function:** File thumbnail extension capability for generating file icon thumbnails (reserved capability, currently unsupported).

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Unspecified

```cangjie
Unspecified
```

**Function:** Unspecified type, used with queryExtensionAbilityInfo interface to query all ExtensionAbility types.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Wallpaper

```cangjie
Wallpaper
```

**Function:** Wallpaper extension capability for implementing desktop wallpapers (reserved capability, currently unsupported).

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Window

```cangjie
Window
```

**Function:** Interface composition extension capability, allowing system applications to launch and embed cross-application interfaces.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### WorkScheduler

```cangjie
WorkScheduler
```

**Function:** Delayed task extension capability, allowing applications to execute non-time-sensitive tasks during system idle periods.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

## enum LaunchType

```cangjie
public enum LaunchType {
    | Singleton
    | Multiton
    | Specified
    | ...
}
```

**Function:** Each capability has a launch type, this enum identifies the launch type of the capability.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Multiton

```cangjie
Multiton
```

**Function:** Capability launches in standard multi-instance mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Singleton

```cangjie
Singleton
```

**Function:** Capability launches in single-instance mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Specified

```cangjie
Specified
```

**Function:** Capability launches in custom multi-instance mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

## enum ModuleType

```cangjie
public enum ModuleType {
    | Entry
    | Feature
    | Shared
    | ...
}
```

**Function:** Identifies module types.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Entry

```cangjie
Entry
```

**Function:** Main module of an application.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Feature

```cangjie
Feature
```

**Function:** Dynamic feature module of an application.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Shared

```cangjie
Shared
```

**Function:** Dynamic shared library module of an application.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

## enum MultiAppModeType

```cangjie
public enum MultiAppModeType {
    | Unspecified
    | MultiInstance
    | AppClone
    | ...
}
```

**Function:** Identifies application multi-launch mode types.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### AppClone

```cangjie
AppClone
```

**Function:** Clone mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### MultiInstance

```cangjie
MultiInstance
```

**Function:** Multi-instance mode.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Unspecified

```cangjie
Unspecified
```

**Function:** Unspecified type.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21## enum PermissionGrantState

```cangjie
public enum PermissionGrantState {
    | PermissionDenied
    | PermissionGranted
    | ...
}
```

**Description:** Indicates the permission grant state.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### PermissionDenied

```cangjie
PermissionDenied
```

**Description:** Permission is denied.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### PermissionGranted

```cangjie
PermissionGranted
```

**Description:** Permission is granted.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

## enum SupportWindowMode

```cangjie
public enum SupportWindowMode {
    | FullScreen
    | Split
    | Floating
    | ...
}
```

**Description:** An ability can support multiple window modes. This enumeration is used to indicate the supported window modes of an ability.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Floating

```cangjie
Floating
```

**Description:** Supports floating window display.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### FullScreen

```cangjie
FullScreen
```

**Description:** Supports full-screen window display.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21

### Split

```cangjie
Split
```

**Description:** Supports split-screen window display.

**System Capability:** SystemCapability.BundleManager.BundleFramework.Core

**Since:** 21