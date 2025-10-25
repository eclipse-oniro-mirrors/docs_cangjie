# module.json5 Configuration File

## Configuration File Example

An example to provide an overall understanding of the module.json5 configuration file.

<!--RP1-->

```json
{
  "module": {
    "name": "entry",
    "type": "entry",
    "description": "$string:module_desc",
    "srcEntry": "ohos_app_cangjie_entry.MyAbilityStage",
    "mainElement": "EntryAbility",
    "deviceTypes": [
      "default",
      "tablet"
    ],
    "deliveryWithInstall": true,
    "installationFree": false,
    "pages": "$profile:main_pages",
    "virtualMachine": "ark",
    "appStartup": "$profile:app_startup_config",
    "metadata": [
      {
        "name": "string",
        "value": "string",
        "resource": "$profile:distributionFilter_config"
      }
    ],
    "abilities": [
      {
        "name": "EntryAbility",
        "srcEntry": "ohos_app_cangjie_entry.MainAbility",
        "description": "$string:EntryAbility_desc",
        "icon": "$media:layered_image",
        "label": "$string:EntryAbility_label",
        "startWindow": "$profile:start_window",
        "startWindowIcon": "$media:icon",
        "startWindowBackground": "$color:start_window_background",
        "exported": true,
        "skills": [
          {
            "entities": [
              "entity.system.home"
            ],
            "actions": [
              "ohos.want.action.home"
            ]
          }
        ],
        "continueType": [
          "continueType1"
        ],
        "continueBundleName": [
          "com.example.myapplication1",
          "com.example.myapplication2"
        ]
      }
    ],
    "definePermissions": [
      {
        "name": "ohos.abilitydemo.permission.PROVIDER",
        "grantMode": "system_grant",
        "availableLevel": "system_core",
        "provisionEnable": true,
        "distributedSceneEnable": false,
        "label": "$string:EntryAbility_label"
      }
    ],
    "requestPermissions": [
      {
        "name": "ohos.abilitydemo.permission.PROVIDER",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "FormAbility"
          ],
          "when": "inuse"
        }
      }
    ],
    "targetModuleName": "feature",
    "targetPriority": 50,
    "querySchemes": [
      "app1Scheme",
      "app2Scheme"
    ],
    "appEnvironments": [
      {
        "name": "name1",
        "value": "value1"
      }
    ],
    "hnpPackages": [
      {
        "package": "hnpsample.hnp",
        "type": "public"
      }
    ],
    "fileContextMenu": "$profile:menu"
  }
}
```

<!--RP1End-->

## Configuration File Tags

The module.json5 configuration file contains the following tags.

**Table 1** Description of module.json5 Configuration File Tags

| Attribute Name | Meaning | Data Type | Optional |
| -------- |-------------------| -------- | -------- |
| name | Identifies the name of the current Module, ensuring uniqueness across the application. Naming rules:<br/>- Consists of letters, numbers, and underscores, and must start with a letter.<br/>- Maximum length is 31 bytes. | String | This tag is mandatory. |
| type | Identifies the type of the current Module. Supported values:<br/>- entry: The main module of the application.<br/>- feature: Dynamic feature module of the application.<br/>- har: Static shared package module.<br/>- shared: Dynamic shared package module. | String | This tag is mandatory. |
| srcEntry | Identifies the class path of the entry UIAbility or ExtensionAbility corresponding to the current Module. Must point to the same UIAbility or ExtensionAbility as the mainElement field. Value is a string not exceeding 127 bytes. | String | This tag is optional, default is empty. |
| description | Describes the current Module. Developers can use this field to describe the module's functionality and purpose. Value is a string not exceeding 255 bytes, which can use string resource indexing for multilingual support. | String | This tag is optional, default is empty. |
| <!--DelRow-->process | Identifies the process name of the current Module. Value is a string not exceeding 31 bytes. If process is configured under the HAP tag, all UIAbility, DataShareExtensionAbility, and ServiceExtensionAbility of this Module will run in this process.<br/>**Note:**<br/>Effective only when [multi-instance privilege](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-app-privilege-config-guide.md) is enabled. Third-party app configurations are not effective. | String | This tag is optional, default is the bundleName under the app tag in the app.json5 file. |
| mainElement | Identifies the name of the entry UIAbility or ExtensionAbility of the current Module. Must point to the same UIAbility or ExtensionAbility as the srcEntry field. Value is a string not exceeding 255 bytes. | String | This tag is optional, default is empty. |
| [deviceTypes](#devicetypes-tag) | Identifies the types of devices on which the current Module can run.<br/>**Note:**<br/>When multiple modules exist, their configurations can differ, but all must include the device types to be installed to ensure proper operation. | String array | This tag is mandatory. |
| deliveryWithInstall | Indicates whether the current Module is installed when the user actively installs it, i.e., whether the HAP corresponding to this Module is installed with the application.<br/>- true: Installed with the application.<br/>- false: Not installed with the application. | Boolean | This tag is mandatory. |
| installationFree | Indicates whether the current Module supports installation-free features.<br/>- true: Supports installation-free features and meets the constraints.<br/>- false: Does not support installation-free features.<br/>**Note:**<br/>When [bundleType](./app-configuration-file.md#configuration-file-tags) is atomic service, this field must be set to true. Otherwise, it must be set to false. | Boolean | This tag is mandatory. |
| [pages](#pages-tag) | Identifies the profile resource of the current Module, used to list page information. Value is a string not exceeding 255 bytes. | String | This tag is mandatory for scenarios with UIAbility. |
| [metadata](#metadata-tag) | Identifies custom metadata of the current Module, which can configure [distributionFilter](#distributionfilter-tag), [shortcuts](#shortcuts-tag), etc., via resource references. Effective only for the current Module, UIAbility, and ExtensionAbility. | Object array | This tag is optional, default is empty. |
| [abilities](#abilities-tag) | Identifies the configuration information of UIAbility in the current Module, effective only for the current UIAbility. | Object array | This tag is optional, default is empty. |
| [extensionAbilities](#extensionabilities-tag) | Identifies the configuration information of ExtensionAbility in the current Module, effective only for the current ExtensionAbility. | Object array | This tag is optional, default is empty. |
| <!--DelRow-->[definePermissions](#definepermissions-tag) | Identifies permissions defined by system resource HAPs. Custom permissions are not supported. | Object array | This tag is optional, default is empty. |
| [requestPermissions](../../security/AccessToken/cj-declare-permissions.md#declaring-permissions-in-the-configuration-file)| Identifies the set of permissions the current application needs to request from the system at runtime. | Object array | This tag is optional, default is empty. |
| [testRunner](#testrunner-tag) | Identifies the configuration of the test framework for testing the current Module. | Object | This tag is optional, default is empty. |
| [dependencies](#dependencies-tag)| Identifies the list of shared libraries the current module depends on at runtime. | Object array | This tag is optional, default is empty. |
| [proxyData](#proxydata-tag) | Identifies the list of data proxies provided by the current Module. | Object array | This tag is optional, default is empty.|
| isolationMode | Identifies the multi-process configuration of the current Module. Supported values:<br/>- nonisolationFirst: Prefer running in a non-independent process.<br/>- isolationFirst: Prefer running in an independent process.<br/>- isolationOnly: Run only in an independent process.<br/>- nonisolationOnly: Run only in a non-independent process.<br/>**Note:**<br/>1. Only 2in1 and tablet devices support setting the current Module to an independent process.<br/>2. This field is effective only for HAPs. | String | This tag is optional, default is nonisolationFirst.|
| generateBuildHash | Indicates whether the current HAP generates a hash value via the packaging tool. When set to true, if the application's versionCode remains unchanged during system OTA upgrades, the hash value can determine whether the application needs an upgrade.<br/>This field is enabled only when the generateBuildHash field in the [app.json5 file](./app-configuration-file.md#appjson5-configuration-file) is false.<br/>**Note:**<br/>This field is effective only for pre-installed applications. | Boolean | This tag is optional, default is false.|
| compressNativeLibs | Indicates whether the libs library is packaged into the HAP in a compressed storage manner.<br/>- true: libs library is stored compressed.<br/>- false: libs library is stored uncompressed. | Boolean | This tag is optional, default is false when packaging HAPs. |
| libIsolation | Indicates whether a directory named after the module is generated under the libs directory to store .so files, distinguishing .so files of different HAPs within the same application to prevent conflicts.<br/>- true: .so files of the current HAP are stored in a directory named after the Module under the libs directory.<br/>- false: .so files of the current HAP are stored directly in the libs directory. | Boolean | This tag is optional, default is false. |
| fileContextMenu | Identifies the right-click menu configuration of the current HAP. Value is a string not exceeding 255 bytes.<br/>**Note:**<br/>Effective only on PC/2in1 devices. | String | This tag is optional, default is empty. |
| querySchemes | Identifies the URL schemes allowed for the current application to perform jump queries. Only entry-type modules can configure this, with a maximum of 50 schemes, each not exceeding 128 bytes. | String array | This tag is optional, default is empty. |
| [appEnvironments](#appenvironments-tag) | Identifies the application environment variables configured for the current module. Only entry and feature modules can configure this. | Object array | This tag is optional, default is empty. |
| appStartup | Identifies the startup framework configuration path of the current Module, effective for Entry-type HAPs and HARs. | String | This tag is optional, default is empty. |
| [hnpPackages](#hnppackages-tag) | Identifies the Native package information included in the current application. Only entry-type modules can configure this. | Object array | This tag is optional, default is empty. |
| abilitySrcEntryDelegator | Identifies the name of the UIAbility to which the current Module needs to redirect, used in combination with the abilityStageSrcEntryDelegator field to specify the redirection target.<br/>**Note:**<br/>1. Supported from API version 17.<br/>2. Cannot be configured in HAR configuration files or redirect to HAR UIAbility. | String | This tag is optional, default is empty. |
| abilityStageSrcEntryDelegator | Identifies the Module name (cannot be the current Module name) of the UIAbility to which the current Module needs to redirect, used in combination with the abilitySrcEntryDelegator field to specify the redirection target.<br/>**Note:**<br/>1. Supported from API version 17.<br/>2. Cannot be configured in HAR configuration files or redirect to HAR UIAbility. | String | This tag is optional, default is empty. |

## deviceTypes Tag

**Table 2** Description of deviceTypes Tag
<!--RP2-->
| Device Type | Enum Value | Description |
| -------- | -------- | -------- |
| Tablet | tablet | - |
| PC/2in1 | 2in1 | PC devices, primarily interacted with via multi-window, multi-task, and keyboard/mouse operations, maximizing productivity. In OpenHarmony documentation, "2in1" represents "PC/2in1". |
| Default Device | default | Devices supporting all system capabilities. |
<!--RP2End-->

deviceTypes Example:

```json
{
  "module": {
    "name": "myHapName",
    "type": "feature",
    "deviceTypes" : [
       "tablet"
    ]
  }
}
```

## pages Tag

This tag is a profile file resource used to specify the configuration file describing page information.

```json
{
  "module": {
    // ...
    "pages": "$profile:main_pages", // Configured via resource files under profile
  }
}
```

Define the configuration file main_pages.json under resources/base/profile in the development view. The filename "main_pages" can be customized but must match the information specified by the pages tag. The configuration file lists the page information of the current application component, including page routing and display window-related configurations.

**Table 3** Description of pages Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- |-----------| -------- | -------- |
| src | Identifies the routing information of all pages in the current Module, including page paths and names. Page paths are relative to the src/main/cangjie directory of the current Module. Value is a string array, with each element representing a page. | String array | This tag is mandatory. |
| window | Identifies configurations related to display windows. | Object | This tag is optional, default is empty. |

**Table 4** Description of window Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- |-----------------|
| designWidth | Identifies the design reference width of the page. Elements are scaled based on this width relative to the actual device width. | Numeric | Optional, default is 720.px. |
| autoDesignWidth | Indicates whether the design reference width is automatically calculated. When set to true, designWidth is ignored, and the design reference width is calculated based on device width and screen density. When set to false, the design reference width is designWidth. | Boolean | Optional, default is false. |

```json
{
  "src": [
    "pages/index/mainPage",
    "pages/second/payment",
    "pages/third/shopping_cart",
    "pages/four/owner"
  ],
  "window": {
    "designWidth": 720,
    "autoDesignWidth": false
  }
}
```

## metadata Tag

This tag identifies custom metadata of the HAP. The tag value is an array type, containing three sub-tags: name, value, and resource.

**Table 5** Description of metadata Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| name | Identifies the name of the data item. Value is a string not exceeding 255 bytes. | String | This tag is optional, default is empty. |
| value | Identifies the value of the data item. Value is a string not exceeding 255 bytes. | String | This tag is optional, default is empty. |
| resource | Identifies custom user data. Value is a string not exceeding 255 bytes, referencing the data resource index. For example, configured as $profile:shortcuts_config, it points to the /resources/base/profile/shortcuts_config.json configuration file. | String | This tag is optional, default is empty. |

Below are two usage scenarios and examples of the metadata tag. Developers can also customize settings based on actual needs.

1. Use the metadata tag to configure the default size and position of the main window (unit: vp). The name values and corresponding meanings are as follows:

    - name set to ohos.ability.window.height represents the default height of the main window, value represents the height.
    - name set to ohos.ability.window.width represents the default width of the main window, value represents the width.
    - name set to ohos.ability.window.left represents the default left position of the main window. value represents the configuration format: alignment +/- offset. Alignment options include center, left, and right, default is left; offset can be omitted if 0.
    - name set to ohos.ability.window.top represents the default top position of the main window. value represents the configuration format: alignment +/- offset. Alignment options include center, top, and bottom, default is top. If both alignment and offset are omitted, the system default stacking rules apply.

2. Use the metadata tag to configure whether to remove the splash screen. Configuration item: name set to enable.remove.starting.window, value set to true or false. true means remove the splash screen, false means keep it. Default is false if not configured.

```json
{
  "module": {
    "metadata": [{
      "name": "module_metadata",
      "value": "a test demo for module metadata",
      "resource": "$profile:shortcuts_config"
    }],

    "abilities": [{
      "metadata": [{
        "name": "ability_metadata",
        "value": "a test demo for ability",
        "resource": "$profile:config_file"
      },
      {
        "name": "ability_metadata_2",
        "value": "a string test",
        "resource": "$profile:config_file"
      },
      {
        "name": "ohos.ability.window.height",
        "value": "987"
      },
      {
        "name": "ohos.ability.window.width",
        "value": "1300"
      },
      {
        "name": "ohos.ability.window.left",
        "value": "right-50"
      },
      {
        "name": "ohos.ability.window.top",
        "value": "center+50"
      },
      {
        "name": "enable.remove.starting.window",
        "value": "true"
      }],
    }],

    "extensionAbilities": [{
      "metadata": [{
        "name": "extensionAbility_metadata",
        "value": "a test for extensionAbility",
## skills Tag

This tag identifies the characteristics of [Want](../../application-models/cj-want-overview.md#Want Overview) that a UIAbility component or ExtensionAbility component can receive.

**Table 7** Description of the skills Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| actions | Identifies the set of Action values that can be received. The values are usually system-predefined action values, but custom values are also allowed.<br>It is not recommended to configure multiple actions in a single skill, as this may result in failure to match the expected scenario. | String array | This tag is optional. The default value is empty. |
| entities | Identifies the set of Entity values that can be received.<br>It is not recommended to configure multiple entities in a single skill, as this may result in failure to match the expected scenario. | String array | This tag is optional. The default value is empty. |
| uris | Identifies the set of URIs (Uniform Resource Identifier) that match the Want. The maximum number of elements in the array is 512. | Object array | This tag is optional. The default value is empty. |
| permissions | Identifies the custom permission information of the current UIAbility component. Other applications accessing this UIAbility must apply for the corresponding permission information.<br/>Each array element is a permission name, which follows the reverse domain name format (not exceeding 255 bytes) and uses system-predefined permissions. | String array | This tag is optional. The default value is empty. |
| domainVerify | Identifies whether domain verification is enabled.<br/>- true: Enables domain verification.<br/>- false: Disables domain verification. | Boolean | This tag is optional. The default value is false. |

**Table 8** Description of the uris Tag

> **Note:**
>
> The following string-type fields do not support configuration via resource indexing (e.g., `$string`).

| Attribute Name | Meaning | Data Type | Optional |
| -------- |-----------------| -------- | -------- |
| scheme | Identifies the protocol part of the URI, such as http, https, file, ftp, etc.<br/>**Note:**<br/>Starting from API 18, this field is case-insensitive during implicit Want matching. | String | Can be omitted only when type is configured in uris. The default value is empty; otherwise, it cannot be omitted. |
| host | Identifies the host address part of the URI. This field takes effect only when scheme is configured. Common formats include:<br/>- Domain name format, e.g., example.com.<br/>- IP address format, e.g., 10.10.10.1.<br/>**Note:**<br/>Starting from API 18, this field is case-insensitive during implicit Want matching. | String | This tag is optional. The default value is empty. |
| port | Identifies the port part of the URI. For example, the default port for http is 80, https is 443, and ftp is 21. This field takes effect only when both scheme and host are configured. | String | This tag is optional. The default value is empty. |
| path \| pathStartWith \| pathRegex | Identifies the path part of the URI. Only one of path, pathStartWith, or pathRegex can be configured. `path` indicates exact matching of the URI path with the Want path, `pathStartWith` indicates prefix matching, and `pathRegex` indicates regular expression matching. This field takes effect only when both scheme and host are configured. | String | This tag is optional. The default value is empty. |
| type | Identifies the data type that matches the Want, using the MIME (Multipurpose Internet Mail Extensions) specification. Can be configured alongside scheme or separately. | String | This tag is optional. The default value is empty. |
| utd | Applicable to scenarios such as sharing. | String | This tag is optional. The default value is empty. |
| maxFileSupported | For specified file types, identifies the maximum number of files that can be received or opened at once. Applicable to scenarios such as sharing and must be used with utd. | Integer | This tag is optional. The default value is 0. |

Example of skills:

```json
{
  "abilities": [
    {
      "skills": [
        {
          "actions": [
            "ohos.want.action.home"
          ],
          "entities": [
            "entity.system.home"
          ],
          "uris": [
            {
              "scheme":"http",
              "host":"example.com",
              "port":"80",
              "path":"path",
              "type": "text/*",
              "linkFeature": "Login"
            }
          ],
          "permissions": [],
          "domainVerify": false
        }
      ]
    }
  ]
}
```

## extensionAbilities Tag

Describes the configuration information of extensionAbilities. The tag value is an array, and the configurations under this tag apply only to the current extensionAbilities.

**Table 9** Description of the extensionAbilities Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- |------------------| -------- | -------- |
| name | Identifies the name of the current ExtensionAbility component, ensuring uniqueness within the application. The value is a string not exceeding 127 bytes. | String | This tag is mandatory. |
| srcEntry | Identifies the class path corresponding to the current ExtensionAbility component. The value is a string not exceeding 127 bytes. | String | This tag is mandatory. |
| description | Describes the current ExtensionAbility component. Developers can use this field to explain the component's functionality and purpose. The value is a string not exceeding 255 bytes and can be a resource index for multilingual support. | String | This tag is optional. The default value is empty. |
| icon | Identifies the icon of the current ExtensionAbility component, using a resource file index. If the ExtensionAbility component is configured as mainElement, this tag must be configured. | String | This tag is optional. The default value is empty. |
| label | Identifies the display name of the current ExtensionAbility component for users. The value is a resource index supporting multilingualism, not exceeding 255 bytes. If the ExtensionAbility is configured as the mainElement of the current Module, this tag must be configured and must be unique within the application. | String | This tag is optional. The default value is empty. |
| type | Identifies the type of the current ExtensionAbility component. Supported values include:<br/>- form: Card-type ExtensionAbility.<br/>- workScheduler: Delayed task ExtensionAbility.<br/>- inputMethod: Input method ExtensionAbility.<br/>- accessibility: Accessibility ExtensionAbility.<br/>- staticSubscriber: Static broadcast ExtensionAbility.<br/>- wallpaper: Wallpaper ExtensionAbility.<br/>- backup: Data backup ExtensionAbility.<br/>- window: This ExtensionAbility creates a window during startup, providing interface development for developers. The developed interface will be integrated into other applications' windows via the UIExtensionComponent control.<br/>- thumbnail: File thumbnail ExtensionAbility, allowing developers to provide thumbnails for custom file types.<br/>- preview: This ExtensionAbility displays parsed files in a window, which can be integrated into other applications' windows.<br/>- print: Printing framework ExtensionAbility.<br/>- push: Push ExtensionAbility.<br/>- driver: Driver framework ExtensionAbility. Applications configured with this type are considered driver applications, which are installed, uninstalled, and restored without distinguishing users. For example, creating a sub-user will automatically install existing driver applications from the main user, and uninstalling a driver application on a sub-user will also uninstall it on the main user.<br/>- remoteNotification: Remote notification ExtensionAbility.<br/>- remoteLocation: Remote location ExtensionAbility.<br/>- voip: VoIP ExtensionAbility.<br/>- action: Custom operation template ExtensionAbility, providing developers with UIExtension-based custom operation templates.<br/>- embeddedUI: Embedded UI ExtensionAbility, providing cross-process interface embedding capabilities.<br/>- insightIntentUI: Provides developers with the ability to be invoked by Xiaoyi's intent and display content in a window.<br/>- ads: Ad ExtensionAbility, used with the AdComponent control to display ad pages in other applications. Only available to device manufacturers.<br/>- photoEditor: Photo editing ExtensionAbility, providing developers with UIExtension-based photo editing templates.<br/>- appAccountAuthorization: App account authorization ExtensionAbility, handling account authorization requests such as login authorization.<br/>- autoFill/password: Account and password auto-fill ExtensionAbility, supporting data saving and filling.<br/>- hms/account: App account management ExtensionAbility.<br/>- autoFill/smart: Contextual auto-fill ExtensionAbility, supporting data saving and filling.<br/>- uiService: Popup service component, creating a window during startup and supporting bidirectional communication.<br/>- statusBarView: One-step access ExtensionAbility.<br/>- recentPhoto: Recent photo recommendation ExtensionAbility. | String | This tag is mandatory. |
| permissions | Identifies custom permission information for the current ExtensionAbility component. Other applications accessing this ExtensionAbility must apply for the corresponding permissions.<br/>Each array element is a permission name, typically in reverse domain name format (max 255 bytes), using [system-predefined permissions](../../security/AccessToken/cj-app-permissions.md). | String array | This tag is optional. The default value is empty. |
| readPermission | Identifies the permission required to read data from the current ExtensionAbility component. The value is a string not exceeding 255 bytes. Only applicable when the ExtensionAbility's type is dataShare. | String | This tag is optional. The default value is empty. |
| writePermission | Identifies the permission required to write data to the current ExtensionAbility component. The value is a string not exceeding 255 bytes. Only applicable when the ExtensionAbility's type is dataShare. | String | This tag is optional. The default value is empty. |
| uri | Identifies the data URI provided by the current ExtensionAbility component. The value is a string array not exceeding 255 bytes, in reverse domain name format.<br/>**Note:**<br/>This tag is mandatory when the ExtensionAbility's type is dataShare. | String | This tag is optional. The default value is empty. |
| skills | Identifies the set of [Want](../../application-models/cj-want-overview.md#Want Overview) characteristics that the current ExtensionAbility component can receive.<br/>Configuration rules: The entry package can configure multiple ExtensionAbilities with entry capabilities (configured with ohos.want.action.home and entity.system.home). The label and icon of the first ExtensionAbility with the skills tag will serve as the service or application's label and icon.<br/>**Note:**<br/>Feature packages for services do not support configuring skills tags with entry capabilities.<br/>Feature packages for applications support configuring skills tags with entry capabilities. | Array | This tag is optional. The default value is empty. |
| [metadata](#metadata-tag) | Identifies metadata for the current ExtensionAbility component.<br/>**Note:**<br/>This tag is mandatory when the type is form, and must include an object value named ohos.extension.form, with a non-optional resource value referencing the secondary resource of the service card. | Object array | This tag is optional. The default value is empty. |
| exported | Identifies whether the current ExtensionAbility component can be invoked by other applications.<br/>- true: Can be invoked by other applications.<br/>- false: Cannot be invoked by other applications, including being launched via the aa tool command. | Boolean | This tag is optional. The default value is false. |
| extensionProcessMode | Identifies the multi-process instance model of the current ExtensionAbility component. Currently only applicable to UIExtensionAbility and its derived ExtensionAbilities.<br/>- instance: Each instance of this ExtensionAbility runs in a separate process.<br/>- type: All instances of this ExtensionAbility run in the same process, separate from other ExtensionAbilities.<br/>- bundle: All instances of this ExtensionAbility run in the application's unified process, sharing the process with other ExtensionAbilities configured with the bundle model.<br>- runWithMainProcess: This ExtensionAbility shares the process with the application's main process. Only one-step access ExtensionAbilities can be configured with runWithMainProcess. | String | This tag is optional. The default value is empty. |
| dataGroupIds | Identifies the dataGroupId set of the current ExtensionAbility component. If the application's certificate in the app market includes a dataGroupId in its groupIds, the ExtensionAbility component can share directories generated by this dataGroupId with the application. Thus, the ExtensionAbility's dataGroupId must be one configured in the application's signing certificate's groupIds field to take effect. This field only applies when the ExtensionAbility has an independent sandbox directory. See [dataGroupId Application Process](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ime-kit-security#section4219152220459). | String array | This tag is optional. The default value is empty. |
| process | Identifies the process label of the component. Only applicable when the type is embeddedUI.<br/>**Note:**<br/>Only effective on [2in1](./module-configuration-file.md#devicetypes-tag) devices. UIAbility and ExtensionAbility components with the same label run in the same process. Supported from API version 14. | String | This tag is optional. The default value is empty. |

Example of extensionAbilities:

```json
{
  "extensionAbilities": [
    {
      "name": "FormName",
      "srcEntry": "ohos_app_cangjie_entry.MainAbility",
      "icon": "$media:icon",
      "label" : "$string:extension_name",
      "description": "$string:form_description",
      "type": "form",
      "permissions": ["ohos.abilitydemo.permission.PROVIDER"],
      "readPermission": "",
      "writePermission": "",
      "exported": true,
      "uri":"scheme://authority/path/query",
      "skills": [{
        "actions": [],
        "entities": [],
        "uris": [],
        "permissions": []
      }],
      "metadata": [
        {
          "name": "ohos.extension.form",
          "resource": "$profile:form_config",
        }
      ],
      "extensionProcessMode": "instance",
      "dataGroupIds": [
        "testGroupId1"
      ]
    }
  ]
}
```

## shortcuts Tag

The shortcuts tag identifies the shortcut information of an application. The tag value is an array containing four sub-tags: shortcutId, label, icon, and wants.

Metadata specifies shortcut information, where:
- name: Specifies the name of the shortcuts, using ohos.ability.shortcuts as the identifier.
- resource: Specifies the resource location of the shortcuts information.

**Table 10** Description of the shortcuts Tag

| Attribute Name | Meaning | Type | Optional |
| -------- | -------- | -------- | -------- |
| shortcutId | Identifies the ID of the shortcut. The value is a string not exceeding 63 bytes. **Does not support configuration via resource indexing (e.g., `$string`).** | String | This tag is mandatory. |
| label | Identifies the label information of the shortcut, i.e., the text description displayed externally. The value is a string not exceeding 255 bytes, which can be descriptive content or a label resource index. | String | This tag is optional. The default value is empty. |
| icon | Identifies the icon of the shortcut, using a resource file index. | String | This tag is optional. The default value is empty. |
| [wants](#wants-tag) | Identifies the set of target wants information defined within the shortcut. When the launcherBundleManager's startShortcut interface is called, the first target component in the wants tag will be launched. It is recommended to configure only one wants element. | Object | This tag is optional. The default value is empty. |

1. Configure the shortcuts_config.json file in the /resources/base/profile/ directory.

   ```json
   {
     "shortcuts": [
       {
         "shortcutId": "id_test1",
         "label": "$string:shortcut",
         "icon": "$media:aa_icon",
         "wants": [
           {
             "bundleName": "com.ohos.hello",
             "moduleName": "entry",
             "abilityName": "EntryAbility",
             "parameters": {
               "testKey": "testValue"
             }
           }
         ]
       }
     ]
   }
   ```

2. In the module.json5 configuration file, configure the metadata tag for the UIAbility that requires shortcuts to make the shortcut configuration effective.

   ```json
   {
     "module": {
       // ...
       "abilities": [
         {
           "name": "EntryAbility",
           "srcEntry": "ohos_app_cangjie_entry.MainAbility",
           // ...
           "skills": [
             {
               "entities": [
                 "entity.system.home"
               ],
               "actions": [
                 "ohos.want.action.home"
               ]
             }
           ],
           "metadata": [
             {
               "name": "ohos.ability.shortcuts",
               "resource": "$profile:shortcuts_config"
             }
           ]
         }
       ]
     }
   }
   ```

### wants Tag

This tag identifies the set of target wants information defined within the shortcut.

**Table 11** Description of the wants Tag

| Attribute Name | Meaning | Type | Optional |
| -------- | -------- | -------- | -------- |
| bundleName | Identifies the target package name of the shortcut. | String | This tag is mandatory. |
| moduleName | Identifies the target module name of the shortcut. | String | This tag is optional. |
| abilityName | Identifies the target component name of the shortcut. | String | This tag is mandatory. |
| parameters | Identifies custom data when launching the shortcut. Only string-type data is supported. Both keys and values support strings up to 1024 bytes in length. | Object | This tag is optional. |

Example of data tag:

```json
{
  "wants": [
    {
      "bundleName": "com.ohos.hello",
      "moduleName": "entry",
      "abilityName": "EntryAbility",
      "parameters": {
        "testKey": "testValue"
      }
    }
  ]
}
```

## distributionFilter Tag

This tag defines the distribution strategy for HAPs corresponding to specific device specifications, enabling precise matching during cloud distribution in the app market.

- **Applicable Scenario:** When a project contains multiple Entries, and the deviceTypes of these Entries overlap, this tag is used to differentiate them. For example, if two Entries both support the tablet type, this tag is needed for differentiation.

   ```json
   // Device types supported by entry1
   {
     "module": {
       "name## proxyData Tag

This tag identifies the list of data proxies provided by the module, applicable only to entry and feature configurations.

**Table 19** Description of the proxyData Tag

| Attribute Name | Meaning | Data Type | Optional |
| ----------- | ------------------------------ | -------- | ---------- |
| uri | Identifies the URI used to access this data proxy. The URIs configured for different data proxies must be unique and must follow the format `datashareproxy://current_application_package_name/xxx`. The value is a string with a maximum length of 255 bytes. | String | This tag cannot be omitted. |
| requiredReadPermission | Identifies the permission required to read data from this data proxy. If not configured, other applications cannot use this proxy. For non-system applications, the permission level must be system_basic or system_core. For system applications, there are no restrictions on the permission level. For permission levels, refer to [Permission List](../../security/AccessToken/cj-app-permissions.md). The value is a string with a maximum length of 255 bytes. | String | This tag is optional, with a default value of empty. |
| requiredWritePermission | Identifies the permission required to write data to this data proxy. If not configured, other applications cannot use this proxy. For non-system applications, the permission level must be system_basic or system_core. For system applications, there are no restrictions on the permission level. For permission levels, refer to [Permission List](../../security/AccessToken/cj-app-permissions.md). The value is a string with a maximum length of 255 bytes. | String | This tag is optional, with a default value of empty. |
| [metadata](#metadata-tag) | Identifies the metadata of this data proxy, supporting only the configuration of name and resource fields. | Object | This tag is optional, with a default value of empty. |

Example of the proxyData tag:

```json
{
  "module": {
    "proxyData": [
      {
        "uri":"datashareproxy://com.ohos.datashare/event/Meeting",
        "requiredReadPermission": "ohos.permission.GET_BUNDLE_INFO",
        "requiredWritePermission": "ohos.permission.GET_BUNDLE_INFO",
        "metadata": {
          "name": "datashare_metadata",
          "resource": "$profile:datashare"
        }
      }
    ]
  }
}
```

## appEnvironments Tag

This tag identifies the application environment variables configured by the module.

**Table 20** Description of the appEnvironments Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| name | Identifies the name of the environment variable. The value is a string with a maximum length of 4096 bytes. | String | This tag is optional, with a default value of empty. |
| value | Identifies the value of the environment variable. The value is a string with a maximum length of 4096 bytes. | String | This tag is optional, with a default value of empty. |

Example of the appEnvironments tag:

```json
{
  "module": {
    "appEnvironments": [
      {
        "name":"name1",
        "value": "value1"
      }
    ]
  }
}
```

## hnpPackages Tag

This tag identifies the Native package information included in the application.

**Table 21** Description of the hnpPackages Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| package | Identifies the name of the Native package. | String | This tag cannot be omitted. |
| type | Identifies the type of the Native package. Supported values are as follows:<br/>-&nbsp;public: Public type.<br/>-&nbsp;private: Private type. | String | This tag cannot be omitted. |

Example of hnpPackages:

```json
{
  "module" : {
    "hnpPackages": [
      {
        "package": "hnpsample.hnp",
        "type": "public"
      }
    ]
  }
}
```

## fileContextMenu Tag

This tag identifies the right-click menu configuration items for the current HAP. It is a profile file resource used to specify the configuration file describing the right-click menu registered by the application. It takes effect only on PC/2-in-1 devices.

Example of the fileContextMenu tag:

```json
{
  "module": {
    // ...
    "fileContextMenu": "$profile:menu" // Configured via the resource file under profile
  }
}
```

The configuration file menu.json is defined under resources/base/profile in the development view. The filename "menu.json" can be customized but must correspond to the information specified in the fileContextMenu tag. The configuration file describes the items and response behaviors of the right-click menu registered by the current application.

The root node of the configuration file is named fileContextMenu, which is an array of objects, indicating the number of right-click menus registered by the current module. (A single module or application cannot register more than 5 menus. If more than 5 are configured, only 5 will be randomly parsed.)

**Table 22** Description of the fileContextMenu Tag Configuration

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| abilityName | Indicates the name of the ability to be launched corresponding to the current right-click menu. | String | Cannot be omitted. |
| menuItem | The information displayed in the right-click menu. Naming suggestions:<br/>Principle 1: [Action] + [App Name], e.g., "Open with {App}", "Open with {App} ({Plugin} plugin)" in Chinese; "Open with {App}", "Open with {App} ({Plugin})" in English.<br/>Principle 2: [Action] + [Purpose], e.g., "Compress to {filename}", "Compress to {path}", "Convert to {format} with {App}". | Resource ID | Cannot be omitted. |
| menuHandler | An ability can create multiple right-click menus. This field is used to distinguish different right-click menu items launched by the user. When the user clicks a right-click menu item, this field will be passed as a parameter to the right-click menu application. | String | Cannot be omitted. |
| menuContext | Defines the context required to display this menu item, supporting multiple scenarios. The type is an array. | Object Array | Cannot be omitted. |

**Table 23** Description of the menuContext Tag Configuration

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| menuKind | Indicates the type of click that triggers the right-click menu. Valid values are:<br/>-&nbsp;0: Blank area<br/>-&nbsp;1: File<br/>-&nbsp;2: Folder<br/>-&nbsp;3: Both file and folder | Number | Cannot be omitted. |
| menuRule | Indicates the method of selecting files or folders that triggers the right-click menu. Valid values are:<br/>-&nbsp;single: Single selection<br/>-&nbsp;multi: Multiple selection<br/>-&nbsp;both: Single or multiple selection | String | This field is read only when menuKind is 1 or 2, and cannot be omitted in such cases. |
| fileSupportType | Indicates that the right-click menu is displayed when the selected file list includes the specified file types.<br/>When this field is set to ["*"], the fileNotSupportType field will be read.<br/>When this field is set to [], no action is taken. | String Array | This field is read only when menuKind is 1, and cannot be omitted in such cases. |
| fileNotSupportType | Indicates that the right-click menu is not displayed when the selected file list includes these file types.<br/>This field is read only when menuKind is 1 and fileSupportType is ["*"]. | String Array | Optional, with a default value of empty. |

Example of the menu.json resource file under resources/base/profile:

```json
{
  "fileContextMenu": [
    {
      "abilityName": "EntryAbility",
      "menuItem": "$string:module_desc",
      "menuHandler": "openCompress",
      "menuContext": [
        {
          "menuKind": 0
        },
        {
          "menuKind": 1,
          "menuRule": "both",
          "fileSupportType": [
            ".rar",
            ".zip"
          ],
          "fileNotSupportType": [
            ""
          ]
        },
        {
          "menuKind": 2,
          "menuRule": "single"
        },
        {
          "menuKind": 3
        }
      ]
    }
  ]
}
```

**Response Behavior**

After an application registers a right-click extension menu, the "More" option will appear in the right-click menu in the file manager. Clicking "More" will display the registered menuItem list. Clicking any option will cause the file manager to launch the third-party application via startAbility by default. In addition to specifying the package name and ability name of the third-party application, the following fields will be passed in the parameter of the want:

**Table 24** Description of the parameter Fields in want

| Parameter Name | Value | Type |
| -------- | -------- | -------- |
| menuHandler | Corresponds to the value of menuHandler in the registration configuration file. | String |
| uriList | The URI value triggered by the user's right-click on a specific file. If triggered in a blank area, this value is empty. For a single file response, the array length is 1. For multiple file responses, the URIs of all corresponding files are passed. | String Array |

## startWindow Tag

This tag points to a profile file resource used to specify the configuration file for the start page of a UIAbility component. The configuration file start_window.json is defined under resources/base/profile in the development view. If this field is configured, the startWindowIcon and startWindowBackground fields will not take effect. Supported from API version 18.

**Table 25** Description of the startWindow Tag Configuration

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| startWindowAppIcon | Identifies the resource file index of the start page icon for the current UIAbility component. The value is a string with a maximum length of 255 bytes. | String | Optional, with a default value of empty. |
| startWindowIllustration | Identifies the resource file index of the start page illustration for the current UIAbility component. The value is a string with a maximum length of 255 bytes. | String | Optional, with a default value of empty. |
| startWindowBrandingImage | Identifies the resource file index of the start page branding image for the current UIAbility component. The value is a string with a maximum length of 255 bytes. | String | Optional, with a default value of empty. |
| startWindowBackgroundColor | Identifies the resource file index of the start page background color for the current UIAbility component. The value is a string with a maximum length of 255 bytes. | String | Cannot be omitted. |
| startWindowBackgroundImage | Identifies the resource file index of the start page background image for the current UIAbility component. The value is a string with a maximum length of 255 bytes. | String | Optional, with a default value of empty. |
| startWindowBackgroundImageFit | Identifies the adaptation method of the start page background image for the current UIAbility component. Supported values are:<br/>-&nbsp;Contain: Scales the image proportionally to fit within the display boundaries.<br/>-&nbsp;Cover: Scales the image proportionally to cover the display boundaries.<br/>-&nbsp;Auto: Adaptive display.<br/>-&nbsp;Fill: Scales the image without maintaining aspect ratio to fill the display boundaries.<br/>-&nbsp;ScaleDown: Scales the image proportionally or keeps it unchanged.<br/>-&nbsp;None: Displays the image at its original size. | String | Optional, with a default value of Cover. |

Example of the start_window.json resource file under resources/base/profile:

```json
{
  "startWindowAppIcon": "$media:start_window_app_icon",
  "startWindowIllustration": "$media:start_window_illustration",
  "startWindowBrandingImage": "$media:start_window_branding_image",
  "startWindowBackgroundColor": "$color:start_window_back_ground_color",
  "startWindowBackgroundImage": "$media:start_window_back_ground_image",
  "startWindowBackgroundImageFit": "Cover"
}
```

## definePermissions Tag

This tag supports only system resource HAPs for defining permissions and does not support application-defined permissions. For permission definition methods, refer to [System Resource Permission Definition](https://gitee.com/openharmony/utils_system_resources/blob/master/systemres/main/config.json).

**Table 26** Description of the definePermissions Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| name | Identifies the name of the permission. The maximum length of this tag is 255 bytes. | String | Cannot be omitted. |
| grantMode | Identifies the granting mode of the permission. Supported modes are:<br/>-&nbsp;system_grant: Automatically granted by the system after installation.<br/>-&nbsp;user_grant: Dynamically requested during use and requires user authorization. | String | Optional, with a default value of system_grant. |
| availableLevel | Identifies the restriction category of the permission. Valid values are:<br/>-&nbsp;system_core: System core permission.<br/>-&nbsp;system_basic: System basic permission.<br/>-&nbsp;normal: Normal permission. Permissions that all applications are allowed to request. | String | Optional, with a default value of normal. |
| provisionEnable | Indicates whether the permission can be requested via certificates, including high-level permissions. true means developers can request permissions via certificates. false means developers cannot request permissions via certificates. | Boolean | Optional, with a default value of true. |
| distributedSceneEnabled | Indicates whether the permission can be used in distributed scenarios. true means developers can use the permission in distributed scenarios. false means developers cannot use the permission in distributed scenarios. | Boolean | Optional, with a default value of false. |
| label | Identifies a brief description of the permission, configured as a resource index of the description content. | String | Optional, with a default value of empty. |
| description | Identifies a detailed description of the permission, which can be a string or a resource index of the description content. | String | Optional, with a default value of empty. |

Example of the definePermissions tag:

```json
{
  "module" : {
    "definePermissions": [
      {
        "name": "ohos.abilitydemo.permission.PROVIDER",
        "grantMode": "system_grant",
        "availableLevel": "system_core",
        "provisionEnable": true,
        "distributedSceneEnable": false,
        "label": "$string:EntryAbility_label"
      }
    ]
  }
}
```

<!--DelEnd-->