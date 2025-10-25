# Unpacking Tool

The unpacking tool is a debugging utility provided by OpenHarmony that supports decompressing HAP, HSP, and App files into folders via command-line operations. It also offers Java interfaces for parsing HAP, HSP, and App files.

The `app_unpacking_tool.jar` used for unpacking can be found in the locally downloaded OpenHarmony SDK library.

> **Note:**
>
> Currently, Cangjie only supports developing HAR and HAP packages but not HSP packages. Therefore, HSP-related functionalities in this tool are unavailable in Cangjie programs.

## Constraints and Limitations

The unpacking tool requires Java 8 or higher to run.

## Unpacking Command Instructions

### HAP Package Mode Unpacking Command

Developers can use the unpacking tool's JAR package to unpack applications by passing unpacking options and file paths to extract HAP packages.

#### Example

```bash
java -jar app_unpacking_tool.jar --mode hap --hap-path <path> --out-path <path> [--force true]
```

#### Parameter Descriptions and Specifications

| Command      | Required | Options       | Description                                                                 |
|--------------|----------|---------------|-----------------------------------------------------------------------------|
| --mode       | Yes      | hap           | Unpacking type.                                                            |
| --hap-path   | Yes      | NA            | Path to the HAP package.                                                   |
| --rpcid      | No       | true or false | Whether to extract only the rpcid file from the HAP package to the specified directory. If true, only the rpcid file is extracted without unpacking the HAP package. |
| --out-path   | Yes      | NA            | Target path for unpacked files.                                             |
| --force      | No       | true or false | Default is false. If true, forces deletion when target files exist.         |

### App Package Mode Unpacking Command

Developers can use the unpacking tool's JAR package to unpack applications by passing unpacking options and file paths to extract App packages.

#### Example

```bash
java -jar app_unpacking_tool.jar --mode app --app-path <path> --out-path <path> [--force true]
```

#### Parameter Descriptions and Specifications

| Command      | Required | Options       | Description                                                                 |
|--------------|----------|---------------|-----------------------------------------------------------------------------|
| --mode       | Yes      | app           | Unpacking type.                                                            |
| --app-path   | Yes      | NA            | Path to the App package.                                                    |
| --out-path   | Yes      | NA            | Target path for unpacked files.                                             |
| --force      | No       | true or false | Default is false. If true, forces deletion when target files exist.         |

### Extracting rpcid File from HAP Package

Developers can use the unpacking tool's JAR package to unpack applications by passing unpacking options and file paths to retrieve the application's rpcid.

#### Example

```bash
java -jar app_unpacking_tool.jar --mode hap --rpcid true --hap-path <path> --out-path <path> [--force true]
```

#### Parameter Descriptions and Specifications

| Command      | Required | Options       | Description                                                                 |
|--------------|----------|---------------|-----------------------------------------------------------------------------|
| --mode       | Yes      | hap           | Unpacking type.                                                            |
| --rpcid      | No       | true or false | Whether to extract only the rpcid file from the HAP package to the specified directory. If true, only the rpcid file is extracted without unpacking the HAP package. |
| --hap-path   | Yes      | NA            | Path to the HAP package.                                                   |
| --out-path   | Yes      | NA            | Target path for the extracted rpcid file.                                    |
| --force      | No       | true or false | Default is false. If true, forces deletion when target files exist.         |

### HSP Package Mode Unpacking Command

Developers can use the unpacking tool's JAR package to unpack applications by passing unpacking options and file paths to extract HSP packages.

#### Example

```bash
java -jar app_unpacking_tool.jar --mode hsp --hsp-path <path> --out-path <path> [--force true]
```

#### Parameter Descriptions and Specifications

| Command      | Required | Options       | Description                                                                 |
|--------------|----------|---------------|-----------------------------------------------------------------------------|
| --mode       | Yes      | hsp           | Unpacking type.                                                            |
| --hsp-path   | Yes      | NA            | Path to the HSP package.                                                   |
| --out-path   | Yes      | NA            | Target path for unpacked files.                                             |
| --force      | No       | true or false | Default is false. If true, forces deletion when target files exist.         |

### APPQF Mode Unpacking Command

Developers can use the unpacking tool's JAR package to unpack applications by passing unpacking options and file paths to extract APPQF packages.

#### Example

```bash
java -jar app_unpacking_tool.jar --mode appqf --appqf-path <path> --out-path <path> [--force true]
```

#### Parameter Descriptions and Specifications

| Command      | Required | Options       | Description                                                                 |
|--------------|----------|---------------|-----------------------------------------------------------------------------|
| --mode       | Yes      | appqf         | Unpacking type.                                                            |
| --appqf-path | Yes      | NA            | Path to the APPQF package.                                                 |
| --out-path   | Yes      | NA            | Target path for unpacked files.                                             |
| --force      | No       | true or false | Default is false. If true, forces deletion when target files exist.         |

## Package Parsing Interfaces

Package parsing interfaces are used only by app markets to parse built HAP, HSP, and App packages to retrieve configuration file information.

### Interface Directory

| Class Name          | Interface Prototype                                                                 | Type     | Detailed Description                                                                 |
|---------------------|------------------------------------------------------------------------------------|----------|-------------------------------------------------------------------------------------|
| UncompressEntrance  | UncompressResult parseApp(String appPath, ParseAppMode parseMode, String hapName)  | Java API | Function: Parses the pack.info information of an App package based on parameters.<br/>Input: appPath (App package path), parseMode (parsing mode enum: ALL/HAP_LIST/HAP_INFO), hapName (HAP package name, required when parseMode is HAP_INFO).<br/>Return: UncompressResult. |
| UncompressEntrance  | UncompressResult parseApp(InputStream input, ParseAppMode parseMode, String hapName) | Java API | Function: Parses the pack.info information of an App package based on parameters.<br/>Input: input (App file stream), parseMode (parsing mode enum: ALL/HAP_LIST/HAP_INFO), hapName (HAP package name, required when parseMode is HAP_INFO).<br/>Return: UncompressResult. |
| UncompressEntrance  | UncompressResult parseHap(String hapPath)                                         | Java API | Function: Parses the JSON configuration file of an App package based on parameters.<br/>Input: hapPath (HAP package path).<br/>Return: UncompressResult. |
| UncompressEntrance  | UncompressResult parseHap(InputStream input)                                      | Java API | Function: Parses the JSON configuration file of an App package based on parameters.<br/>Input: input (HAP package file stream).<br/>Return: UncompressResult. |

## Unpacking Tool Information Fields

### UncompressResult (Bundle Information) Structure

| Field           | Type               | Description                                                                 | Note |
|-----------------|--------------------|-----------------------------------------------------------------------------|------|
| result          | boolean            | Indicates whether the parsing was successful. true for success, false for failure. | NA   |
| message         | String             | Failure reason returned when parsing fails.                                  | NA   |
| packInfos       | List\<PackInfo>    | packages information from the bundle's pack.info file.                      | NA   |
| profileInfos    | List\<ProfileInfo> | Application configuration information.                                      | NA   |
| profileInfosStr | List\<String>      | Application configuration information.                                      | NA   |
| icon            | String             | Returns the icon path of the entry component. If no entry component exists, returns the first component's icon information. | NA   |
| label           | String             | Returns the label of the entry component. If no entry component exists, returns the first component's label information. | NA   |
| packageSize     | long               | Indicates the size of the App package in bytes.                            | NA   |

### PackInfo Structure

| Field                | Type          | Description                                                                 | Note |
|----------------------|---------------|-----------------------------------------------------------------------------|------|
| name                 | String        | Package name.                                                              | NA   |
| moduleName           | String        | HAP name.                                                                  | NA   |
| moduleType           | String        | Module type.                                                               | NA   |
| deviceType           | List\<String> | Device types supported by the current HAP package.                         | NA   |
| deliveryWithInstall  | boolean       | Indicates whether the current HAP is installed when the user actively installs it. true for installation, false otherwise. | NA   |

### ProfileInfo Structure

| Field         | Type                           | Description                                                                 | Note |
|---------------|---------------------------------|-----------------------------------------------------------------------------|------|
| hapName       | String                         | Name of the current HAP package being parsed.                              | NA   |
| appInfo       | AppInfo structure              | Structure identifying App information (see AppInfo below).                 | NA   |
| deviceConfig  | Map\<String, DeviceConfig>     | Device information.                                                        | Stored as Map\<String, String>, containing device type names and corresponding information. In the stage model, this field is stored in the app structure. |
| hapInfo       | HapInfo structure              | Module information in the HAP package (see HapInfo below).                | NA   |

### AppInfo Structure

| Field                           | Type     | Description                                                                 | Note |
|---------------------------------|----------|-----------------------------------------------------------------------------|------|
| bundleName                      | String   | App package name.                                                          | NA   |
| vendor                          | String   | App vendor information.                                                    | NA   |
| relatedBundleName               | String   | Related bundle package name.                                               | NA   |
| versionName                     | String   | versionName information in the App.                                        | NA   |
| versionCode                     | String   | versionCode information in the App.                                        | NA   |
| targetApiVersion                | int      | API target version required for the application to run.                    | NA   |
| compatibleApiVersion            | int      | API version compatible with the application.                               | NA   |
| appName                         | String   | Label displayed on the desktop for the ability.                           | NA   |
| appNameEN                       | String   | Label displayed on the desktop for the ability.                             | NA   |
| releaseType                     | String   | Type of API target version required for the application.                   | NA   |
| shellVersionCode                | String   | API version number of the application.                                    | NA   |
| shellVersionName                | String   | API version name of the application.                                       | NA   |
| multiFrameworkBundle            | boolean  | Application framework. true for hybrid packaging, false otherwise.         | NA   |
| debug                           | boolean  | Whether the application is debuggable. true for debuggable, false otherwise. | NA   |
| icon                            | String   | Application icon path.                                                    | NA   |
| label                           | String   | Application label.                                                        | NA   |
| description                     | String   | Application description.                                                   | Added in the stage model. |
| minCompatibleVersionCode        | int      | Minimum compatible version number of the application.                      | NA   |
| distributedNotificationEnabled  | boolean  | Whether the application enables distributed notifications. true for enabled, false otherwise. | Added in the stage model. |
| bundleType                      | String   | Bundle type: <br/>- app: Application.<br/>- atomicService: Atomic service.<br/>- shared: Shared library between applications. | NA   |
| compileSdkVersion               | String   | SDK version used to compile the application.                               | Only for applications with API 10 and above. |
| compileSdkType                  | String   | SDK category used to compile the application.                              | Only for applications with API 10 and above. |
| labels                          | HashMap\<String, String> | Multilingual labels for the AppJson application.                           | NA   |
| descriptions                    | HashMap\<String, String> | Multilingual descriptions for the AppJson application.                     | NA   |

### HapInfo Structure

| Field                 | Type                        | Description                                                                 | Note |
|-----------------------|-----------------------------|-----------------------------------------------------------------------------|------|
| appModel              | AppModel enum               | Application framework model.<br/>- FA: FA model.<br/>- STAGE: Stage model. | NA   |
| packageStr            | String                      | Package information of the application.                                    | FA model only. |
| name                  | String                      | Name of the current module.                                                | NA   |
| description           | String                      | Description of the HAP package.                                            | FA model only. |
| supportedModes        | List\<String>               | Supported modes of the HAP package.                                        | NA   |
| abilities             | List\<AbilityInfo>          | Ability information in the HAP package.                                    | NA   |
| defPermissions        | List\<DefPermission>        | DefPermission information in the HAP package.                              | NA   |
| definePermissions     | List\<DefinePermission>     | DefinePermission information in the HAP package.                           | NA   |
| defPermissionsGroups  | List\<DefPermissionsGroups> | DefPermissionsGroups information in the HAP package.                       | NA   |
| distro                | Distro structure            | Distro information of the HAP package.                                     | NA   |
| reqCapabilities       | List\<String>               | reqCapabilities information in the HAP package.                            | NA   |
| deviceType            | List\<String>               | Device types on which the HAP can run.                                    | Corresponds to deviceTypes in the stage model. |
| metaData              | MetaData structure          | Custom metadata of the HAP.                                               | NA   |
| dependencies          | List\<DependencyItem>       | DependencyItem information in the HAP package.                             | NA   |
| isJs                  | boolean                     | Whether the application is a JS application. true for JS, false otherwise. | FA model only. |
| reqPermissions        | List\<ReqPermission>        | Collection of permissions requested by the application.                   | Corresponds to requestPermissions in the stage model. |
| commonEvents          | CommonEvent structure        | Static events.                                                             | NA   |
| shortcuts             | List\<Shortcut>             | Shortcuts information of the application.                                  | NA   |
| distroFilter          | DistroFilter structure      | Information for app market distribution by device type.                   | NA   |
| srcEntrance           | String                      | Entry code path of the application.                                       | Added in the stage model. |
| process               | String                      | Process name of the HAP.                                                  | Added in the stage model. |
| mainElement           | String                      | Entry ability or extension name of the HAP.                               | Added in the stage model. FA model assigns mainAbility value to mainElement. |
| uiSyntax              | String                      | Syntax type of the JS Component.                                          | Added in the stage model. |
| pages                 | List\<String>               | Page information in the JS Component.                                     | Added in the stage model. |
| extensionAbilityInfos | List\<ExtensionAbilityInfo> | Configuration information of extensionAbility.                            | Added in the stage model. |
| moduleAtomicService   | ModuleAtomicService structure | Atomic service information of the HAP.                                    | NA   |
| formInfos             | List\<AbilityFormInfo>       | Card information.                                                         | NA   |
| descriptions          | HashMap\<String, String>     | Description information of the HAP.                                       | NA   |
| compressedSize        | long                         | Compressed size of the HAP package in bytes.                              | NA   |
| originalSize          | long                         | Original size of the HAP package in bytes.                                | NA   |

### AbilityInfo Structure

| Field              | Type                       | Description                                                                 | Note |
|--------------------|----------------------------|-----------------------------------------------------------------------------|------|
| name               | String                     | Logical name of the current ability.                                       | NA   |
| description        | String                     | Description of the ability.                                                | NA   |
| descriptionRes     | String                     | Resource description of the ability.                                        | NA   |
| icon               | String                     | Icon of the ability.                                                      | NA   |
| iconPath           | String                     | Icon path of the ability.                                                  | NA   |
| label              | String                     | Name displayed to users for the ability.                                   | NA   |
| labelRes           | String                     | Resource name displayed to users for the ability.                          | NA   |
| type               | String                     | Type of the ability.                                                       | In the stage model, this value is directly assigned as the page type. |
| formsEnabled       | boolean                    | Whether the ability card is enabled. true for enabled, false otherwise.   | NA   |
| formInfo           | FormInfo structure          | Card information.                                                         | NA   |
| uri                | String                     | URI information of the ability.                                           | FA model only. |
| launchType         | String                     | launcherType information of the ability.                                   | NA   |
| orientation        | String                     | orientation information of the ability.                                    | NA   |
| visible            | boolean                    | visible information of the ability. true for visible, false otherwise.    | NA   |
| grantPermission    | boolean                    | grantPermission information of the ability.                               | NA   |
| readPermission     | String                     | readPermission information of the ability.                                 | NA   |
| writePermission    | String                     | writePermission information of the ability.                               | NA   |
| uriPermissionMode  | String                     | uriPermissionMode information of the ability.                             | NA   |
| uriPermissionPath  | String                     | uriPermissionPath information of the ability.                             | NA   |
| directLaunch       | boolean                    | directLaunch information of the ability.                                  | NA   |
| mission            | String                     | mission information of the ability.                                       | NA   |
| targetAbility      | String                     | targetAbility information of the ability.                                 | NA   |
| multiUserShared    | boolean                    | multiUserShared information of the ability. true for supporting multi-user state sharing, false otherwise. | NA   |
| supportPipMode     | boolean                    | supportPipMode information of the ability.### UriInfo Structure Information

| Field          | Type   | Description                     | Remarks |
| -------------- | ------ | ------------------------------- | ------- |
| schema         | String | Identifies the schema information of ModuleUriInfo. | NA      |
| host           | String | Identifies the host information of ModuleUriInfo. | NA      |
| port           | String | Identifies the port information of ModuleUriInfo. | NA      |
| pathStartWith  | String | Identifies the path prefix of ModuleUriInfo. | NA      |
| pathRegex      | String | Identifies the path regex information of ModuleUriInfo. | NA      |
| path           | String | Identifies the path information of ModuleUriInfo. | NA      |
| type           | String | Identifies the type of ModuleUriInfo. | NA      |

### AbilityFormInfo Structure Information

| Field                 | Type                     | Description                                                                 | Remarks |
| --------------------- | ------------------------ | --------------------------------------------------------------------------- | ------- |
| name                  | String                   | Identifies the name of the form.                                            | NA      |
| type                  | String                   | Identifies the type of the card.                                            | NA      |
| updateEnabled         | boolean                  | Indicates whether the card supports scheduled refresh. `true` means supported, `false` means not supported. | NA      |
| scheduledUpdateTime   | String                   | Identifies the scheduled refresh time of the card, using 24-hour format with minute precision. | NA      |
| updateDuration        | int                      | Identifies the refresh interval of the card, in units of 30 minutes (must be a multiple of 30). | NA      |
| supportDimensions     | List\<String>            | Identifies the card appearance specifications, with values such as "1 * 2", "2 * 2", "2 * 4", "4 * 4". | NA      |
| defaultDimension      | String                   | Identifies the default appearance specification of the card, which must be in the `supportDimensions` list. | NA      |
| MetaData              | MetaData                 | Identifies custom information of the card.                                  | NA      |
| description           | String                   | Identifies the description of the form.                                    | Added in the stage model. |
| src                   | String                   | Identifies the UI code corresponding to the JS card.                        | NA      |
| windowInfo            | ModuleWindowInfo structure | Identifies the window of the ability form.                                | NA      |
| isDefault             | boolean                  | Indicates whether the card is the default card. Each HAP can have only one default card. `true` means default, `false` means non-default. | NA      |
| colorMode             | String                   | Identifies the color mode of the card, with values `auto`, `dark`, or `light`. | NA      |
| formConfigAbility     | String                   | Identifies the name of the ability for card adjustment.                     | NA      |
| formVisibleNotify     | String                   | Indicates whether the card is allowed to use visibility notifications.     | NA      |
| providerAbility       | String                   | Identifies the ability or extension name where the card provider resides.<br/>1. FA model: If the card is configured in a service-type ability, `providerAbility` is set to `mainAbility`.<br/>2. FA model: If the card is configured in a page-type ability, `providerAbility` is set to the current ability.<br/>3. FA model: If `mainAbility` is not configured, `providerAbility` is set to `system.home` if available; otherwise, the first page-type ability in the HAP.<br/>4. Stage model (follows the above rules), `providerAbility` is set to `mainElement`. | NA |
| descriptions          | HashMap\<String, String> | Identifies the description of the ability in multiple languages.           | NA      |

### CommonEvent Structure Information

| Field       | Type          | Description                                                                 | Remarks |
| ----------- | ------------- | --------------------------------------------------------------------------- | ------- |
| name        | String        | Identifies the class name of the current static common event.               | For the stage model, obtained from the `staticSubscriber`-type Extension. |
| permission  | String        | Identifies the permission required to implement this static common event.   | For the stage model, obtained from the `staticSubscriber`-type Extension. |
| data        | List\<String> | Identifies the extra data array required for the current static common event. | For the stage model, obtained from the `staticSubscriber`-type Extension. |
| type        | List\<String> | Identifies the category array of the current static common event.           | For the stage model, obtained from the `staticSubscriber`-type Extension. |
| events      | List\<String> | Identifies the set of intent `event` values that can be received.           | For the stage model, obtained from the `staticSubscriber`-type Extension. |

### DependencyItem Structure Information

| Field        | Type   | Description                     | Remarks |
| ------------ | ------ | ------------------------------- | ------- |
| bundleName   | String | Identifies the bundle name of the shared package. | NA      |
| moduleName   | String | Identifies the module name of the shared package. | NA      |
| versionCode  | String | Identifies the version number of the shared package. | NA      |

### ModuleAtomicService Structure Information

| Field         | Type               | Description           | Remarks |
| ------------- | ------------------ | --------------------- | ------- |
| preloadItems  | list\<PreloadItem> | Identifies preload objects. | NA      |

### PreloadItem Structure Information

| Field       | Type   | Description           | Remarks |
| ----------- | ------ | --------------------- | ------- |
| moduleName  | String | Identifies the module name to preload. | NA      |

### DeviceConfig Structure Information

| Field                           | Type    | Description                                                                 | Remarks |
| ------------------------------- | ------- | --------------------------------------------------------------------------- | ------- |
| targetReqSdk                    | String  | Identifies the target requested SDK version of the application's DeviceConfig. | NA      |
| compatibleReqSdk                | String  | Identifies the compatible requested SDK version of the application's DeviceConfig. | NA      |
| jointUserid                     | String  | Identifies the `jointUserid` of the application's DeviceConfig.             | NA      |
| process                         | String  | Identifies the process of the application's DeviceConfig.                   | NA      |
| arkFlag                         | String  | Identifies the `arkFlag` of the application's DeviceConfig.                 | NA      |
| targetArkVersion                | String  | Identifies the `targetArkVersion` of the application's DeviceConfig.        | NA      |
| compatibleArkVersion            | String  | Identifies the compatible ArkVersion of the application's DeviceConfig.     | NA      |
| directLaunch                    | boolean | Identifies the direct launch setting of the application's DeviceConfig.     | NA      |
| distributedNotificationEnabled  | boolean | Identifies the `distributedNotificationEnabled` setting in AppJson. `true` means distributed notifications are enabled, `false` means disabled. | NA      |

### DefPermission Structure Information

| Field           | Type                     | Description                                      | Remarks |
| --------------- | ------------------------ | ------------------------------------------------ | ------- |
| name            | String                   | Identifies the name of the DefPermission.        | NA      |
| grantMode       | String                   | Identifies the `grantMode` of the DefPermission. | NA      |
| group           | String                   | Identifies the group of the DefPermission.       | NA      |
| label           | String                   | Identifies the label of the DefPermission.       | NA      |
| description     | String                   | Identifies the description of the DefPermission. | NA      |
| availableScope  | List\<String>            | Identifies the available scope of the DefPermission. | NA      |
| labels          | HashMap\<String, String> | Identifies the labels of the DefPermission in multiple languages. | NA      |
| descriptions    | HashMap\<String, String> | Identifies the descriptions of the DefPermission in multiple languages. | NA      |

### DefinePermission Structure Information

| Field                   | Type                     | Description                                                                 | Remarks |
| ----------------------- | ------------------------ | --------------------------------------------------------------------------- | ------- |
| name                    | String                   | Identifies the name of the DefinePermission.                                | NA      |
| grantMode               | String                   | Identifies the `grantMode` of the DefinePermission.                        | NA      |
| availableLevel          | String                   | Identifies the group of the DefinePermission.                              | NA      |
| provisionEnable         | boolean                  | Indicates whether the module-defined permission supports certificate-based application. `true` means supported, `false` means not supported. | NA      |
| distributedSceneEnable  | boolean                  | Identifies the `distributedSceneEnable` setting of ModuleDefinePermissions. `true` means the permission can be used in distributed scenarios, `false` means it cannot. | NA      |
| label                   | String                   | Identifies the label of the DefinePermission.                              | NA      |
| description             | String                   | Identifies the description of the DefinePermission.                        | NA      |
| descriptions            | HashMap\<String, String> | Identifies the descriptions of the DefinePermission in multiple languages. | NA      |
| labels                  | HashMap\<String, String> | Identifies the labels of the DefinePermission in multiple languages.       | NA      |

### DefPermissionsGroups Structure Information

| Field        | Type    | Description                         | Remarks |
| ------------ | ------- | ----------------------------------- | ------- |
| name         | String  | Identifies the name of the DefPermissionGroup. | NA      |
| order        | String  | Identifies the order of the DefPermissionGroup. | NA      |
| icon         | String  | Identifies the icon of the DefPermissionGroup. | NA      |
| label        | String  | Identifies the label of the DefPermissionGroup. | NA      |
| description  | String  | Identifies the description of the DefPermissionGroup. | NA      |
| request      | boolean | Identifies the request setting of the DefPermissionGroup. | NA      |

### FormInfo Structure Information

| Field          | Type          | Description                     | Remarks |
| -------------- | ------------- | ------------------------------- | ------- |
| formEntity     | List\<String> | Identifies the `formEntity` of FormInfo. | NA      |
| minHeight      | String        | Identifies the minimum height of FormInfo. | NA      |
| defaultHeight  | String        | Identifies the default height of FormInfo. | NA      |
| minWidth       | String        | Identifies the minimum width of FormInfo. | NA      |
| defaultWidth   | String        | Identifies the default width of FormInfo. | NA      |

### ModuleMetadataInfo Structure Information

| Field     | Type    | Description                         | Remarks |
| --------- | ------- | ----------------------------------- | ------- |
| name      | String  | Identifies the name of ModuleMetadataInfo. | NA      |
| value     | String  | Identifies the value of ModuleMetadataInfo. | NA      |
| resource  | String  | Identifies the resource of ModuleMetadataInfo. | NA      |

### ModuleWindowInfo Structure Information

| Field            | Type    | Description                                | Remarks |
| ---------------- | ------- | ------------------------------------------ | ------- |
| designWidth      | int     | Identifies the design width of the module's used scene. | NA      |
| autoDesignWidth  | boolean | Identifies the `autoDesignWidth` setting of ModuleUsedScene. | NA      |