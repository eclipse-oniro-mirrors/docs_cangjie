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

**Table 1** module.json5 Configuration File Tag Descriptions

| Attribute Name | Description | Data Type | Optional |
| -------- |-------------------| -------- | -------- |
| name | Identifies the name of the current Module, ensuring uniqueness within the application. Naming rules:<br/>- Consists of letters, numbers, and underscores, and must start with a letter.<br/>- Maximum length is 31 bytes. | String | This tag is mandatory. |
| type | Identifies the type of the current Module. Supported values:<br/>- entry: The main module of the application.<br/>- feature: Dynamic feature module of the application.<br/>- har: Static shared package module.<br/>- shared: Dynamic shared package module. | String | This tag is mandatory. |
| srcEntry | Identifies the class path of the entry UIAbility or ExtensionAbility for the current Module. Must point to the same UIAbility or ExtensionAbility as the mainElement field. Value is a string not exceeding 127 bytes. | String | This tag is optional, default is empty. |
| description | Describes the current Module's functionality and purpose. Value is a string not exceeding 255 bytes, which can use string resource indexing for multilingual support. | String | This tag is optional, default is empty. |
| <!--DelRow-->process | Identifies the process name of the current Module. Value is a string not exceeding 31 bytes. If process is configured under the HAP tag, all UIAbility, DataShareExtensionAbility, and ServiceExtensionAbility of this Module will run in this process.<br/>**Note:**<br/>Effective only when [multi-instance privilege](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-app-privilege-config-guide.md) is enabled. Third-party app configurations are not effective. | String | This tag is optional, default is the bundleName under the app tag in app.json5. |
| mainElement | Identifies the entry UIAbility or ExtensionAbility name for the current Module. Must point to the same UIAbility or ExtensionAbility as the srcEntry field. Value is a string not exceeding 255 bytes. | String | This tag is optional, default is empty. |
| [deviceTypes](#devicetypes-tag) | Identifies the types of devices the current Module can run on.<br/>**Note:**<br/>When multiple modules exist, their configurations can differ but must include the device type to be installed for proper operation. | String Array | This tag is mandatory. |
| deliveryWithInstall | Indicates whether the current Module is installed when the user actively installs it, i.e., whether the HAP corresponding to this Module is installed with the application.<br/>- true: Installed with the application.<br/>- false: Not installed with the application. | Boolean | This tag is mandatory. |
| installationFree | Indicates whether the current Module supports installation-free features.<br/>- true: Supports installation-free features and meets the constraints.<br/>- false: Does not support installation-free features.<br/>**Note:**<br/>When [bundleType](./app-configuration-file.md#configuration-file-tags) is atomic service, this field must be set to true. Otherwise, it must be set to false. | Boolean | This tag is mandatory. |
| [pages](#pages-tag) | Identifies the profile resource of the current Module, listing each page's information. Value is a string not exceeding 255 bytes. | String | This tag is mandatory for scenarios with UIAbility. |
| [metadata](#metadata-tag) | Identifies custom metadata for the current Module, configurable via resource references for [distributionFilter](#distributionfilter-tag), [shortcuts](#shortcuts-tag), etc. Effective only for the current Module, UIAbility, and ExtensionAbility. | Object Array | This tag is optional, default is empty. |
| [abilities](#abilities-tag) | Identifies the configuration information of UIAbility in the current Module, effective only for the current UIAbility. | Object Array | This tag is optional, default is empty. |
| [extensionAbilities](#extensionabilities-tag) | Identifies the configuration information of ExtensionAbility in the current Module, effective only for the current ExtensionAbility. | Object Array | This tag is optional, default is empty. |
| <!--DelRow-->[definePermissions](#definepermissions-tag) | Identifies permissions defined by system resource HAPs. Custom permissions are not supported. | Object Array | This tag is optional, default is empty. |
| [requestPermissions](../../security/AccessToken/cj-declare-permissions.md#declare-permissions-in-the-configuration-file)| Identifies the set of permissions the current application needs to request from the system at runtime. | Object Array | This tag is optional, default is empty. |
| [testRunner](#testrunner-tag) | Identifies the configuration of the test framework for testing the current Module. | Object | This tag is optional, default is empty. |
| [dependencies](#dependencies-tag)| Identifies the list of shared libraries the current module depends on at runtime. | Object Array | This tag is optional, default is empty. |
| [proxyData](#proxydata-tag) | Identifies the list of data proxies provided by the current Module. | Object Array | This tag is optional, default is empty.|
| isolationMode | Identifies the multi-process configuration of the current Module. Supported values:<br/>- nonisolationFirst: Prefers running in a non-isolated process.<br/>- isolationFirst: Prefers running in an isolated process.<br/>- isolationOnly: Runs only in an isolated process.<br/>- nonisolationOnly: Runs only in a non-isolated process.<br/>**Note:**<br/>1. Only 2in1 and tablet devices support setting the current Module to an isolated process.<br/>2. This field is effective only for HAPs. |String|This tag is optional, default is nonisolationFirst.|
| generateBuildHash | Indicates whether the current HAP generates a hash value via the packaging tool. When set to true, if the application's versionCode remains unchanged during system OTA updates, the hash value can determine whether the application needs an update.<br/>This field is enabled only when the generateBuildHash field in [app.json5 file](./app-configuration-file.md#appjson5-configuration-file) is false.<br/>**Note:**<br/>This field is effective only for pre-installed applications. |Boolean|This tag is optional, default is false.|
| compressNativeLibs | Indicates whether the libs library is packaged into the HAP in a compressed storage manner when packaging the HAP.<br/>- true: libs library is stored compressed.<br/>- false: libs library is stored uncompressed. | Boolean | This tag is optional, default is false when packaging HAPs. |
| libIsolation | Indicates whether a module-named directory is generated under the libs directory to store .so files, distinguishing .so files of different HAPs within the same application to prevent conflicts.<br/>- true: .so files of the current HAP are stored in a module-named path under the libs directory.<br/>- false: .so files of the current HAP are stored directly in the libs directory. | Boolean | This tag is optional, default is false. |
| fileContextMenu | Identifies the right-click menu configuration of the current HAP. Value is a string not exceeding 255 bytes.<br/>**Note:**<br/>Effective only on PC/2in1 devices. | String | This tag is optional, default is empty. |
| querySchemes | Identifies the URL schemes allowed for the current application's jump queries. Only entry-type modules can configure this, with a maximum of 50 schemes, each not exceeding 128 bytes. | String Array | This tag is optional, default is empty. |
| [appEnvironments](#appenvironments-tag) | Identifies the application environment variables configured for the current module. Only entry and feature modules can configure this. | Object Array | This tag is optional, default is empty. |
| appStartup | Identifies the startup framework configuration path of the current Module, effective for Entry-type HAPs and HARs. | String | This tag is optional, default is empty. |
| [hnpPackages](#hnppackages-tag) | Identifies the Native package information included in the current application. Only entry-type modules can configure this. | Object Array | This tag is optional, default is empty. |
| abilitySrcEntryDelegator | Identifies the UIAbility name to which the current Module needs to redirect, used in combination with the abilityStageSrcEntryDelegator field to specify the redirection target.<br/>**Note:**<br/>1. Supported from API version 17.<br/>2. Cannot be configured in HAR configuration files or redirect to HAR UIAbility. | String | This tag is optional, default is empty. |
| abilityStageSrcEntryDelegator | Identifies the Module name (cannot be the current Module name) to which the current Module needs to redirect its UIAbility, used in combination with the abilitySrcEntryDelegator field to specify the redirection target.<br/>**Note:**<br/>1. Supported from API version 17.<br/>2. Cannot be configured in HAR configuration files or redirect to HAR UIAbility. | String | This tag is optional, default is empty. |

## deviceTypes Tag

**Table 2** deviceTypes Tag Description
<!--RP2-->
| Device Type | Enum Value | Description |
| -------- | -------- | -------- |
| Tablet | tablet | - |
| PC/2in1 | 2in1 | PC devices, primarily interacted with via multi-window, multi-task, and keyboard/mouse operations, maximizing productivity. In OpenHarmony documentation, all "2in1" refers to "PC/2in1". |
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

This tag is a profile file resource specifying the configuration file describing page information.

```json
{
  "module": {
    // ...
    "pages": "$profile:main_pages", // Configured via profile resource file
  }
}
```

Define the configuration file main_pages.json under resources/base/profile in the development view, where the filename "main_pages" can be customized but must match the pages tag specification. The configuration file lists page information within the current application component, including routing and display window configurations.

**Table 3** pages Tag Description

| Attribute Name | Description | Data Type | Optional |
| -------- |-----------| -------- | -------- |
| src | Identifies routing information for all pages in the current Module, including page paths and names. Page paths are relative to the current Module's src/main/cangjie. Value is a string array, with each element representing a page. | String Array | This tag is mandatory. |
| window | Identifies configurations related to display windows. | Object | This tag is optional, default is empty. |

**Table 4** window Tag Description

| Attribute Name | Description | Data Type | Optional  |
| -------- | -------- | -------- |-----------------|
| designWidth | Identifies the baseline width for page design. Elements are scaled based on this and the actual device width. | Number | Optional, default is 720.px. |
| autoDesignWidth | Indicates whether the baseline width is auto-calculated. When true, designWidth is ignored, and the baseline width is calculated from device width and screen density. When false, the baseline width is designWidth. | Boolean | Optional, default is false. |

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

This tag identifies custom metadata for the HAP, with an array value containing name, value, and resource sub-tags.

**Table 5** metadata Tag Description

| Attribute Name | Description | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| name | Identifies the data item name. Value is a string not exceeding 255 bytes. | String | This tag is optional, default is empty. |
| value | Identifies the data item value. Value is a string not exceeding 255 bytes. | String | This tag is optional, default is empty. |
| resource | Identifies custom user data. Value is a string not exceeding 255 bytes, referencing the data resource index, e.g., $profile:shortcuts_config points to /resources/base/profile/shortcuts_config.json. | String | This tag is optional, default is empty. |

Below are two usage scenarios and examples for the metadata tag. Developers can also customize settings based on actual needs.

1. Use metadata to configure the main window's default size and position (in vp units). name values and meanings:
    - ohos.ability.window.height: Default window height, value is the height.
    - ohos.ability.window.width: Default window width, value is the width.
    - ohos.ability.window.left: Default left position. Value format: alignment +/- offset. Alignment options: center, left, right (default left); offset 0 can be omitted.
    - ohos.ability.window.top: Default top position. Value format: alignment +/- offset. Alignment options: center, top, bottom (default top). If both alignment and offset are omitted, system default stacking rules apply.

2. Use metadata to configure whether to remove the splash screen. Configuration: name is enable.remove.starting.window, value is true or false. true removes the splash screen, false does not (default false).

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
        "resource": "$profile:config_file"
      },
      {
        "name": "extensionAbility_metadata_2",
        "value": "a string test",
        "resource": "$profile:config_file"
      }],
    }]
  }
}
```

## abilities Tag

The abilities tag describes the configuration of UIAbility components, with an array value effective only for the current UIAbility.

**Table 6** abilities Tag Description

| Attribute Name | Description   | Data Type | Optional |
|----------|---------------| -------- | -------- |
| srcEntry  | Identifies## skills Tag

This tag identifies the characteristics of [Want](../../application-models/cj-want-overview.md#Want Overview) that a UIAbility component or ExtensionAbility component can receive.

**Table 7** Description of the skills Tag

| Attribute Name | Description | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| actions | Identifies the set of Action values that can be received. The values are usually system-predefined action values, but custom values are also allowed.<br>It is not recommended to configure multiple actions in a single skill, as this may lead to mismatches with expected scenarios. | String array | This tag is optional. The default value is empty. |
| entities | Identifies the set of Entity values that can be received.<br>It is not recommended to configure multiple entities in a single skill, as this may lead to mismatches with expected scenarios. | String array | This tag is optional. The default value is empty. |
| uris | Identifies the set of URIs (Uniform Resource Identifier) that match the Want. The maximum number of elements in the array is 512. | Object array | This tag is optional. The default value is empty. |
| permissions | Identifies custom permission information for the current UIAbility component. Other applications accessing this UIAbility must request the corresponding permissions.<br/>Each array element is a permission name, formatted in reverse domain name style (not exceeding 255 bytes), with values being system-predefined permissions. | String array | This tag is optional. The default value is empty. |
| domainVerify | Identifies whether domain verification is enabled.<br/>- true: Enables domain verification.<br/>- false: Disables domain verification. | Boolean | This tag is optional. The default value is false. |

**Table 8** Description of the uris Tag

> **Note:**
>
> The following string-type fields do not support configuration via resource indexing (e.g., `$string`).

| Attribute Name | Description | Data Type | Optional |
| -------- | ----------------- | -------- | -------- |
| scheme | Identifies the protocol part of the URI, such as http, https, file, ftp, etc.<br/>**Note:**<br/>Starting from API 18, this field is case-insensitive during implicit Want matching. | String | Optional when only `type` is configured in `uris`. The default value is empty. Otherwise, it is mandatory. |
| host | Identifies the host address part of the URI. This field takes effect only when `scheme` is configured. Common formats:<br/>- Domain name format, e.g., example.com.<br/>- IP address format, e.g., 10.10.10.1.<br/>**Note:**<br/>Starting from API 18, this field is case-insensitive during implicit Want matching. | String | This tag is optional. The default value is empty. |
| port | Identifies the port part of the URI. For example, the default port for http is 80, https is 443, and ftp is 21. This field takes effect only when both `scheme` and `host` are configured. | String | This tag is optional. The default value is empty. |
| path \| pathStartWith \| pathRegex | Identifies the path part of the URI. Only one of `path`, `pathStartWith`, or `pathRegex` can be configured. `path` requires exact matching of the URI path with the Want path, `pathStartWith` allows prefix matching, and `pathRegex` allows regular expression matching. This field takes effect only when both `scheme` and `host` are configured. | String | This tag is optional. The default value is empty. |
| type | Identifies the data type matching the Want, using MIME (Multipurpose Internet Mail Extensions) type specifications. Can be configured alongside `scheme` or separately. | String | This tag is optional. The default value is empty. |
| utd | Applicable to scenarios such as sharing. | String | This tag is optional. The default value is empty. |
| maxFileSupported | For specified file types, identifies the maximum number of files that can be received or opened at once. Applicable to scenarios such as sharing and requires `utd` to be configured. | Integer | This tag is optional. The default value is 0. |

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
              "scheme": "http",
              "host": "example.com",
              "port": "80",
              "path": "path",
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

| Attribute Name | Description | Data Type | Optional |
| -------- | ------------------- | -------- | -------- |
| name | Identifies the name of the current ExtensionAbility component, ensuring uniqueness within the application. The value is a string not exceeding 127 bytes. | String | This tag is mandatory. |
| srcEntry | Identifies the class path corresponding to the current ExtensionAbility component. The value is a string not exceeding 127 bytes. | String | This tag is mandatory. |
| description | Describes the current ExtensionAbility component's functionality and purpose. The value is a string not exceeding 255 bytes, which can be a resource index for multilingual support. | String | This tag is optional. The default value is empty. |
| icon | Identifies the icon of the current ExtensionAbility component, referencing a resource file index. Must be configured if the ExtensionAbility component is set as `mainElement`. | String | This tag is optional. The default value is empty. |
| label | Identifies the display name of the current ExtensionAbility component for users, referencing a resource index for multilingual support. The string length must not exceed 255 bytes. Must be configured if the ExtensionAbility is set as the `mainElement` of the current Module, and must be unique within the application. | String | This tag is optional. The default value is empty. |
| type | Identifies the type of the current ExtensionAbility component. Supported values include:<br/>- form: Card ExtensionAbility.<br/>- workScheduler: Delayed task ExtensionAbility.<br/>- inputMethod: Input method ExtensionAbility.<br/>- accessibility: Accessibility ExtensionAbility.<br/>- staticSubscriber: Static broadcast ExtensionAbility.<br/>- wallpaper: Wallpaper ExtensionAbility.<br/>- backup: Data backup ExtensionAbility.<br/>- window: This ExtensionAbility creates a window during startup, providing interface development capabilities. The developed interface can be embedded into other applications' windows via the UIExtensionComponent control.<br/>- thumbnail: File thumbnail ExtensionAbility, allowing developers to provide thumbnails for custom file types.<br/>- preview: This ExtensionAbility parses and displays files in a window, which can be embedded into other applications' windows.<br/>- print: Printing framework ExtensionAbility.<br/>- push: Push ExtensionAbility.<br/>- driver: Driver framework ExtensionAbility. Applications configured with this type are considered driver applications, which are installed, uninstalled, and restored without distinguishing users. For example, creating a sub-user will automatically install driver applications existing on the primary user.<br/>- remoteNotification: Remote notification ExtensionAbility.<br/>- remoteLocation: Remote location ExtensionAbility.<br/>- voip: VoIP ExtensionAbility.<br/>- action: Custom operation business template ExtensionAbility, providing UIExtension-based custom operation templates.<br/>- embeddedUI: Embedded UI ExtensionAbility, enabling cross-process UI embedding.<br/>- insightIntentUI: Provides content display capabilities for intent calls by XiaoYi.<br/>- ads: Ad business ExtensionAbility, used with AdComponent to display ad pages in other applications. Only for device manufacturers.<br/>- photoEditor: Photo editing business ExtensionAbility, providing UIExtension-based photo editing templates.<br/>- appAccountAuthorization: App account authorization ExtensionAbility, handling authorization requests such as login.<br/>- autoFill/password: Auto-fill ExtensionAbility for accounts and passwords, supporting data saving and filling.<br/>- hms/account: App account management ExtensionAbility.<br/>- autoFill/smart: Context-aware auto-fill ExtensionAbility, supporting data saving and filling.<br/>- uiService: Popup service component, creating a window during startup and supporting bidirectional communication.<br/>- statusBarView: One-step access ExtensionAbility.<br/>- recentPhoto: Recent photo recommendation ExtensionAbility. | String | This tag is mandatory. |
| permissions | Identifies custom permission information for the current ExtensionAbility component. Other applications accessing this ExtensionAbility must request the corresponding permissions.<br/>Each array element is a permission name, typically in reverse domain name format (max 255 bytes), with values being [system-predefined permissions](../../security/AccessToken/cj-app-permissions.md). | String array | This tag is optional. The default value is empty. |
| readPermission | Identifies the permission required to read data from the current ExtensionAbility component. The value is a string not exceeding 255 bytes. Only supported when the ExtensionAbility's `type` is `dataShare`. | String | This tag is optional. The default value is empty. |
| writePermission | Identifies the permission required to write data to the current ExtensionAbility component. The value is a string not exceeding 255 bytes. Only supported when the ExtensionAbility's `type` is `dataShare`. | String | This tag is optional. The default value is empty. |
| uri | Identifies the data URI provided by the current ExtensionAbility component, formatted in reverse domain name style (max 255 bytes).<br/>**Note:**<br/>This tag is mandatory when the ExtensionAbility's `type` is `dataShare`. | String | This tag is optional. The default value is empty. |
| skills | Identifies the set of [Want](../../application-models/cj-want-overview.md#Want Overview) characteristics that the current ExtensionAbility component can receive.<br/>Configuration rules: The entry package can configure multiple ExtensionAbilities with entry capabilities (configured with `ohos.want.action.home` and `entity.system.home`). The first ExtensionAbility with a `skills` tag will have its `label` and `icon` used as the service or application's label and icon.<br/>**Note:**<br/>Feature packages for services do not support configuring ExtensionAbilities with entry capabilities.<br/>Feature packages for applications support configuring ExtensionAbilities with entry capabilities. | Array | This tag is optional. The default value is empty. |
| [metadata](#metadata Tag) | Identifies metadata for the current ExtensionAbility component.<br/>**Note:**<br/>This tag is mandatory when `type` is `form`, and must include an object value named `ohos.extension.form`, whose `resource` field cannot be omitted, referencing a secondary resource for service cards. | Object array | This tag is optional. The default value is empty. |
| exported | Identifies whether the current ExtensionAbility component can be called by other applications.<br/>- true: Can be called by other applications.<br/>- false: Cannot be called by other applications, including being launched via the `aa` tool command. | Boolean | This tag is optional. The default value is false. |
| extensionProcessMode | Identifies the multi-process instance model for the current ExtensionAbility component. Currently only applies to UIExtensionAbility and its derived ExtensionAbilities.<br/>- instance: Each instance runs in a separate process.<br/>- type: All instances run in the same process, separate from other ExtensionAbilities.<br/>- bundle: All instances run in the application's unified process, sharing the process with other ExtensionAbilities configured with the `bundle` model.<br>- runWithMainProcess: Runs in the same process as the application's main process. Only one-step access ExtensionAbilities can configure `runWithMainProcess`. | String | This tag is optional. The default value is empty. |
| dataGroupIds | Identifies the set of `dataGroupId` for the current ExtensionAbility component. If the application's certificate includes a `dataGroupId` in the `groupIds` field, the ExtensionAbility can share directories generated by this `dataGroupId`. The ExtensionAbility's `dataGroupId` must match one in the application's certificate to take effect. Only applies when the ExtensionAbility has an independent sandbox directory. | String array | This tag is optional. The default value is empty. |
| process | Identifies the process label for the component. Only configurable when `type` is `embeddedUI`.<br/>**Note:**<br/>Only effective on [2in1](./module-configuration-file.md#devicetypes Tag) devices. UIAbility and ExtensionAbility components with the same label run in the same process. Supported from API version 14. | String | This tag is optional. The default value is empty. |

Example of extensionAbilities:

```json
{
  "extensionAbilities": [
    {
      "name": "FormName",
      "srcEntry": "ohos_app_cangjie_entry.MainAbility",
      "icon": "$media:icon",
      "label": "$string:extension_name",
      "description": "$string:form_description",
      "type": "form",
      "permissions": ["ohos.abilitydemo.permission.PROVIDER"],
      "readPermission": "",
      "writePermission": "",
      "exported": true,
      "uri": "scheme://authority/path/query",
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

The `shortcuts` tag identifies shortcut information for an application. The tag value is an array containing four sub-tags: `shortcutId`, `label`, `icon`, and `wants`.

Metadata specifies shortcut information, where:
- `name`: Specifies the shortcut name, using `ohos.ability.shortcuts` as the identifier.
- `resource`: Specifies the resource location for shortcut information.

**Table 10** Description of the shortcuts Tag

| Attribute Name | Description | Type | Optional |
| -------- | -------- | -------- | -------- |
| shortcutId | Identifies the shortcut ID, a string not exceeding 63 bytes. **Does not support resource indexing (e.g., `$string`).** | String | This tag is mandatory. |
| label | Identifies the shortcut label, i.e., the text description displayed to users. The value is a string not exceeding 255 bytes, which can be descriptive text or a resource index for the label. | String | This tag is optional. The default value is empty. |
| icon | Identifies the shortcut icon, referencing a resource file index. | String | This tag is optional. The default value is empty. |
| [wants](#wants Tag) | Identifies the target `wants` information collection within the shortcut. When calling `launcherBundleManager.startShortcut`, the first target component in the `wants` tag will be launched. It is recommended to configure only one `wants` element. | Object | This tag is optional. The default value is empty. |

1. Configure the `shortcuts_config.json` file in the `/resources/base/profile/` directory.

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

2. In the `module.json5` configuration file, configure the `metadata` tag for the UIAbility that requires shortcuts to make the shortcut configuration effective.

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

This tag identifies the target `wants` information collection within a shortcut.

**Table 11** Description of the wants Tag

| Attribute Name | Description | Type | Optional |
| -------- | -------- | -------- | -------- |
| bundleName | Identifies the target package name for the shortcut. | String | This tag is mandatory. |
| moduleName | Identifies the target module name for the shortcut. | String | This tag is optional. |
| abilityName | Identifies the target component name for the shortcut. | String | This tag is mandatory. |
| parameters | Custom data for launching the shortcut, supporting only string-type data. Both keys and values support strings up to 1024 bytes in length. | Object | This tag is optional. |

Example of the `wants` tag:

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

This tag defines the distribution strategy for HAPs corresponding to specific device specifications, enabling precise matching during cloud distribution via the application market.

- **Use Case:** When a project contains multiple Entry modules with overlapping `deviceTypes`, this tag is used to differentiate them. For example, if two Entry modules both support the `tablet` type, this tag is required for differentiation.

   ```json
   // Entry1 supported device types
   {
     "module": {
       "name": "entry1",
       "type": "entry",
       "deviceTypes": [
         "2in1",
         "tablet"
       ]
     }
   }
   ```

   ```json
   // Entry2 supported device types
   {
     "module":## proxyData Tag

This tag identifies the list of data proxies provided by the module, applicable only to entry and feature configurations.

**Table 19** Description of the proxyData Tag

| Attribute Name | Meaning | Data Type | Optional |
| ----------- | ------------------------------ | -------- | ---------- |
| uri | Identifies the URI for accessing this data proxy. URIs configured for different data proxies must be unique and must follow the format `datashareproxy://current_application_package_name/xxx`. The value is a string with a maximum length of 255 bytes. | String | This attribute is mandatory. |
| requiredReadPermission | Specifies the permission required to read data from this data proxy. If not configured, other applications cannot use this proxy. For non-system applications, the permission level must be system_basic or system_core. System applications have no restrictions on permission levels. For permission levels, refer to [Permission List](../../security/AccessToken/cj-app-permissions.md). The value is a string with a maximum length of 255 bytes. | String | Optional, default is empty. |
| requiredWritePermission | Specifies the permission required to write data to this data proxy. If not configured, other applications cannot use this proxy. For non-system applications, the permission level must be system_basic or system_core. System applications have no restrictions on permission levels. For permission levels, refer to [Permission List](../../security/AccessToken/cj-app-permissions.md). The value is a string with a maximum length of 255 bytes. | String | Optional, default is empty. |
| [metadata](#metadata-tag) | Specifies the metadata for this data proxy, supporting only the name and resource fields. | Object | Optional, default is empty. |

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

This tag identifies the application environment variables configured for the module.

**Table 20** Description of the appEnvironments Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| name | Specifies the name of the environment variable. The value is a string with a maximum length of 4096 bytes. | String | Optional, default is empty. |
| value | Specifies the value of the environment variable. The value is a string with a maximum length of 4096 bytes. | String | Optional, default is empty. |

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
| package | Specifies the name of the Native package. | String | Mandatory. |
| type | Specifies the type of the Native package. Supported values:<br/>- public: Public type.<br/>- private: Private type. | String | Mandatory. |

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

This tag identifies the right-click menu configuration for the current HAP, referencing a profile file resource that specifies the configuration for registering right-click menus. It takes effect only on PC/2-in-1 devices.

Example of the fileContextMenu tag:

```json
{
  "module": {
    // ...
    "fileContextMenu": "$profile:menu" // Configured via the resource file under profile
  }
}
```

The configuration file menu.json is defined under resources/base/profile in the development view. The filename "menu.json" can be customized but must match the information specified in the fileContextMenu tag. The configuration file describes the items and actions of the right-click menu registered by the current application.

The root node of the configuration file is fileContextMenu, an array of objects indicating the number of right-click menus registered by the current module. (A single module or application cannot register more than 5 menus; exceeding this limit will result in only 5 randomly selected menus being parsed.)

**Table 22** Configuration Description of the fileContextMenu Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| abilityName | Specifies the name of the ability to be launched for the current right-click menu. | String | Mandatory. |
| menuItem | The information displayed for the right-click menu. Naming suggestions:<br/>Principle 1: [Action] + [App Name], e.g., "Open with {App}", "Open with {App} ({Plugin} plugin)" in Chinese; "Open with {App}", "Open with {App} ({Plugin})" in English.<br/>Principle 2: [Action] + [Purpose], e.g., "Compress to {filename}", "Compress to {path}", "Convert to {format} with {App}". | Resource ID | Mandatory. |
| menuHandler | An ability can create multiple right-click menus. This field distinguishes between different menu items triggered by the user. When a user clicks a menu item, this field is passed as a parameter to the right-click menu application. | String | Mandatory. |
| menuContext | Defines the context required to display the menu item, supporting multiple scenarios. Type is an array of objects. | Object Array | Mandatory. |

**Table 23** Configuration Description of the menuContext Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| menuKind | Specifies the type of click that triggers the right-click menu. Valid values:<br/>- 0: Blank area<br/>- 1: File<br/>- 2: Folder<br/>- 3: Both file and folder | Number | Mandatory. |
| menuRule | Specifies the file or folder selection method that triggers the right-click menu. Valid values:<br/>- single: Single selection<br/>- multi: Multiple selection<br/>- both: Single or multiple selection | String | Required only when menuKind is 1 or 2. |
| fileSupportType | Specifies that the right-click menu is displayed when the selected file list includes the specified file types.<br/>If this field is set to ["*"], the fileNotSupportType field will be read.<br/>If this field is set to [], no action is taken. | String Array | Required only when menuKind is 1. |
| fileNotSupportType | Specifies that the right-click menu is not displayed when the selected file list includes these file types.<br/>Only read when menuKind is 1 and fileSupportType is ["*"]. | String Array | Optional, default is empty. |

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

After an application registers a right-click extension menu, the file manager will display the "More" option in the right-click menu. Clicking "More" will show the registered menuItem list. Selecting any option will trigger the file manager to launch the third-party application via startAbility. In addition to specifying the package name and ability name of the third-party application, the following fields will be passed in the want parameter:

**Table 24** Description of the parameter Fields in want

| Parameter Name | Value | Type |
| -------- | -------- | -------- |
| menuHandler | Corresponds to the menuHandler value in the registration configuration file. | String |
| uriList | The URI value of the file(s) where the user triggered the right-click. If triggered on a blank area, this value is empty. For a single file, the array length is 1. For multiple files, the URIs of all selected files are included. | String Array |

## startWindow Tag

This tag references a profile file resource that specifies the configuration for the UIAbility component's startup page. The configuration file start_window.json is defined under resources/base/profile in the development view. If this field is configured, the startWindowIcon and startWindowBackground fields will not take effect. Supported from API version 18.

**Table 25** Configuration Description of the startWindow Tag

| Attribute Name | Meaning | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| startWindowAppIcon | Specifies the resource index for the startup page icon of the current UIAbility component. The value is a string with a maximum length of 255 bytes. | String | Optional, default is empty. |
| startWindowIllustration | Specifies the resource index for the startup page illustration of the current UIAbility component. The value is a string with a maximum length of 255 bytes. | String | Optional, default is empty. |
| startWindowBrandingImage | Specifies the resource index for the startup page branding image of the current UIAbility component. The value is a string with a maximum length of 255 bytes. | String | Optional, default is empty. |
| startWindowBackgroundColor | Specifies the resource index for the startup page background color of the current UIAbility component. The value is a string with a maximum length of 255 bytes. | String | Mandatory. |
| startWindowBackgroundImage | Specifies the resource index for the startup page background image of the current UIAbility component. The value is a string with a maximum length of 255 bytes. | String | Optional, default is empty. |
| startWindowBackgroundImageFit | Specifies the adaptation method for the startup page background image of the current UIAbility component. Supported values:<br/>- Contain: Scales the image proportionally to fit within the display boundaries.<br/>- Cover: Scales the image proportionally to cover the display boundaries.<br/>- Auto: Adaptive display.<br/>- Fill: Scales the image without maintaining aspect ratio to fill the display boundaries.<br/>- ScaleDown: Scales the image proportionally to fit or remain unchanged.<br/>- None: Displays the image at its original size. | String | Optional, default is Cover. |

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
| name | Specifies the name of the permission. The maximum length is 255 bytes. | String | Mandatory. |
| grantMode | Specifies the permission grant mode. Supported values:<br/>- system_grant: Automatically granted by the system after installation.<br/>- user_grant: Dynamically requested during use, requiring user authorization. | String | Optional, default is system_grant. |
| availableLevel | Specifies the permission restriction category. Valid values:<br/>- system_core: System core permission.<br/>- system_basic: System basic permission.<br/>- normal: Normal permission. Permissions that all applications can request. | String | Optional, default is normal. |
| provisionEnable | Indicates whether the permission can be requested via certificates, including high-level permissions. true means developers can request permissions via certificates. false means they cannot. | Boolean | Optional, default is true. |
| distributedSceneEnabled | Indicates whether the permission can be used in distributed scenarios. true means developers can use the permission in distributed scenarios. false means they cannot. | Boolean | Optional, default is false. |
| label | Specifies a brief description of the permission, configured as a resource index for the description content. | String | Optional, default is empty. |
| description | Specifies a detailed description of the permission, which can be a string or a resource index for the description content. | String | Optional, default is empty. |

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