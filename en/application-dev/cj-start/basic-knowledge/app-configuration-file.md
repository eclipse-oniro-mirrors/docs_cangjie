# app.json5 Configuration File

## Configuration File Example

First, let's gain an overall understanding of the app.json5 configuration file through an example.

```json
{
  "app": {
    "bundleName": "com.application.myapplication",
    "vendor": "example",
    "versionCode": 1000000,
    "versionName": "1.0.0",
    "icon": "$media:layered_image",
    "label": "$string:app_name",
    "description": "$string:description_application",
    "minAPIVersion": 9,
    "targetAPIVersion": 9,
    "apiReleaseType": "Release",
    "debug": false,
    "car": {
      "minAPIVersion": 8
    },
    "targetBundleName": "com.application.test",
    "targetPriority": 50,
    "appEnvironments": [
      {
        "name":"name1",
        "value": "value1"
      }
    ],
    "maxChildProcess": 5,
    "multiAppMode": {
      "multiAppModeType": "multiInstance",
      "maxCount": 5
    },
    "hwasanEnabled": false,
    "ubsanEnabled": false,
    "cloudFileSyncEnabled": false,
    "configuration": "$profile:configuration",
    "assetAccessGroups": [
      "com.ohos.photos",
      "com.ohos.screenshot",
      "com.ohos.note"
    ]
  },
}
```

## Configuration File Tags

The app.json5 configuration file contains the following tags.

**Table 1** Description of app.json5 Configuration File Tags

| Attribute Name | Description | Data Type | Optional |
| -------- |--------------------------| -------- | -------- |
| bundleName | Identifies the Bundle name of the application, used to uniquely identify the application. Naming rules are as follows:<br/>- Must be a string separated by dots (.), with at least three segments. Each segment can only contain English letters, numbers, and underscores (_).<br/>- The first segment must start with an English letter, while non-first segments must start with a number or English letter. Each segment must end with a number or English letter.<br/>- Consecutive dots (.) are not allowed.<br/>- The minimum string length is 7 bytes, and the maximum is 128 bytes.<br/>- It is recommended to use reverse domain name notation (e.g., "com.example.demo", where the first level is the domain suffix com, the second level is the vendor/personal name, and the third level is the application name, with additional levels possible).<br/>For applications compiled with system source code, it is recommended to name them in the form "com.ohos.demo", where "ohos" identifies system applications. | String | This tag is mandatory. |
| bundleType| Identifies the Bundle type of the application, used to distinguish between applications and atomic services. Supported values are:<br/>- app: The current Bundle is an application.<br/>- atomicService: The current Bundle is an atomic service.<br/>- shared: The current Bundle is a shared library application (reserved field).<br/>- appService: The current Bundle is a system-level shared library application, only for system applications. | String| This tag is optional, with a default value of "app". |
| debug | Indicates whether the application can be debugged.<br/>- true: Debuggable, typically used during development.<br/>- false: Not debuggable, typically used during release. | Boolean | Generated during compilation by DevEco Studio. This tag is optional, with a default value of "false". |
| icon | Identifies the [application icon](../../application-models/cj-application-component-configuration-stage.md#图标和标签配置), with the value being the index of the icon resource file. | String | This tag is mandatory. |
| label | Identifies the [application name](../../application-models/cj-application-component-configuration-stage.md#应用包名配置), with the value being the index of a string resource. The string length must not exceed 63 bytes. | String | This tag is mandatory. |
| description | Identifies the description of the application, with the value being a string resource index of no more than 255 bytes. This field can be used to display application information, such as on the About page of the application. | String | This tag is optional, with a default value of empty. |
| vendor | Identifies the description of the application developer, with the value being a string of no more than 255 bytes. This field can be used to display developer information, such as on the About page of the application. | String | This tag is optional, with a default value of empty. |
| versionCode | Identifies the version number of the application, with the value being a positive integer less than 2^31. This number is only used to determine whether one version is newer than another, with higher numbers indicating newer versions.<br/>Developers can set this value to any positive integer but must ensure that new versions use larger values than older ones. | Number | This tag is mandatory. |
| versionName | Identifies the version number displayed to users.<br/>The value is a string of no more than 127 bytes, consisting only of numbers and dots. The recommended format is "A.B.C.D" (four segments). The meanings of the four segments are as follows:<br/>First segment: Major version number (0–99), indicating significant changes such as major new features or overhauls.<br/>Second segment: Minor version number (0–99), indicating notable features or major bug fixes.<br/>Third segment: Feature version number (0–99), indicating planned new features.<br/>Fourth segment: Patch version number (0–999), indicating maintenance releases such as bug fixes. | String | This tag is mandatory. |
| minCompatibleVersionCode | Identifies the minimum historical version number compatible with the application, used for cross-device collaboration, data migration, and compatibility checks. This is a reserved field and currently unused. The value range is 0–2147483647. | Number | This tag is optional, with a default value equal to the versionCode tag. |
| minAPIVersion | Identifies the minimum API version of the SDK required to run the application. The value range is 0–2147483647. | Number | This tag is automatically generated during application compilation, corresponding to the compatibleSdkVersion tag in the project-level build-profile.json5 file. |
| targetAPIVersion | Identifies the target API version required to run the application. The value range is 0–2147483647. | Number | This tag is automatically generated during application compilation, corresponding to the compileSdkVersion tag in the project-level build-profile.json5 file. |
| apiReleaseType | Identifies the type of the target API version, represented as a string. Values can be "CanaryN", "BetaN", or "Release", where N is a positive integer.<br/>- Canary: Restricted release version.<br/>- Beta: Publicly released Beta version.<br/>- Release: Publicly released stable version. | String | Automatically generated during compilation based on the SDK's Stage. Manual configurations will be overwritten during compilation. |
| accessible | Indicates whether the application can access its installation directory. Only applies to system and pre-installed applications using the Stage model.<br/>- true: The application can access its installation directory.<br/>- false: The application cannot access its installation directory. | Boolean | This tag is optional, with a default value of "false". |
| multiProjects | Indicates whether the current project supports multi-project collaborative development.<br/>- true: The current project supports multi-project collaborative development. Refer to [Multi-Project Build](https://developer.huawei.com/consumer/en/doc/harmonyos-guides/ide-hvigor-multi-projects).<br/>- false: The current project does not support multi-project collaborative development. | Boolean | This tag is optional, with a default value of "false". |
| asanEnabled | Indicates whether the application enables ASAN detection, used to assist in locating crashes caused by buffer overflows.<br/>- true: ASAN detection is enabled.<br/>- false: ASAN detection is disabled. | Boolean | This tag is optional, with a default value of "false". |
| tablet | Specifies special configurations for tablet devices. Configurable attributes include minAPIVersion.<br/>If this attribute is configured for tablet devices, the application will use the configured values on tablets and ignore the values in the common area of app.json5. | Object | This tag is optional. If omitted, tablet devices use the values configured in the common area of app.json5. |
| default | Specifies special configurations for default devices. Configurable attributes include minAPIVersion.<br/>If this attribute is configured for default devices, the application will use the configured values on default devices and ignore the values in the common area of app.json5. | Object | This tag is optional. If omitted, default devices use the values configured in the common area of app.json5. |
| targetBundleName| Identifies the target application specified by the current package. The value rules and range are the same as the bundleName tag. Applications configured with this field have overlay characteristics. | String | This tag is optional, with a default value of empty. |
| targetPriority| Identifies the priority of the current application, with a value range of 1–100. This field can only be configured after targetBundleName is set. | Number | This tag is optional, with a default value of 1. |
| generateBuildHash | Indicates whether all HAPs of the current application generate hash values during packaging.<br/>When set to true, all HAPs under the application will generate corresponding hash values during packaging. During OTA updates, if the versionCode remains unchanged, the system can determine whether the application needs an update based on the hash values.<br/>- true: All HAPs under the application will generate hash values.<br/>- false: All HAPs under the application will not generate hash values.<br/>**Note:**<br/>This field only applies to pre-installed applications. | Boolean | This tag is optional, with a default value of "false". |
| [appEnvironments](#appenvironments-tag) | Identifies the application environment variables configured for the current module. | Array of Objects | This tag is optional, with a default value of empty. |
| maxChildProcess | Identifies the maximum number of child processes that the current application can create. The value range is 0–512, where 0 means unlimited. If the application has multiple modules, the configuration of the entry module takes precedence. | Number | This tag is optional. If omitted, the system default value is used. |
| [multiAppMode](#multiappmode-tag) | Identifies the multi-instance mode configuration of the current application. Only applicable to entry or feature modules of applications with bundleType "app". If multiple modules exist, the entry module configuration takes precedence. | Object | This tag is optional, with a default value of empty. |
| cloudFileSyncEnabled | Indicates whether the current application enables cloud file synchronization.<br/>- true: Cloud file synchronization is enabled.<br/>- false: Cloud file synchronization is disabled. | Boolean | This tag is optional, with a default value of "false". |
| [configuration](#configuration-tag) | Identifies the ability of the current application to adjust font size according to system settings.<br/>This tag is a profile file resource, specifying the configuration file for font size adjustments. | String | This tag is optional. If omitted, the configuration defaults to not following system settings. |
| assetAccessGroups | Configures the Group ID of the application, which, together with the Developer ID, forms the group information.<br/>When packaging HAPs, DevEco signs the group information using the developer certificate, where the group information consists of Developer ID (assigned by the app market) + Group ID (configured by the developer).<br/>**Note:** <br/>This field is supported starting from API version 18. | Array of Strings | This tag is optional, with a default value of empty. |

## appEnvironments Tag

This tag identifies the environment variables configured for the application. During runtime, applications may depend on third-party libraries that use custom environment variables. To avoid modifying the implementation logic of these libraries, custom environment variables can be set in the project configuration file for runtime use.

**Table 2** Description of appEnvironments Tag

| Attribute Name | Description | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| name | Identifies the name of the environment variable. The value is a string of no more than 4096 bytes. | String  | This tag is optional, with a default value of empty. |
| value         | Identifies the value of the environment variable. The value is a string of no more than 4096 bytes.       | String  | This tag is optional, with a default value of empty. |

Example of appEnvironments tag:

```json
{
  "app": {
    "appEnvironments": [
      {
        "name":"name1",
        "value": "value1"
      }
    ]
  }
}
```

## multiAppMode Tag

Application multi-instance mode.

**Table 3** Description of multiAppMode Tag

| Attribute Name | Description | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| multiAppModeType | Identifies the type of multi-instance mode. Supported values are:<br/>- multiInstance: Multi-instance mode. This field is only supported on 2-in-1 devices and does not apply to resident processes.<br/>- appClone: Application clone mode. | String  | This tag is mandatory. |
| maxCount | Identifies the maximum number of allowed multi-instance copies. Supported values are:<br/>- multiInstance mode: 1–10.<br/>- appClone mode: 1–5.      | Number  | This tag is mandatory. |

Example of multiAppMode tag:

```json
{
  "app": {
    "multiAppMode": {
      "multiAppModeType": "appClone",
      "maxCount": 5
    }
  }
}
```

## configuration Tag

This tag is a profile file resource, specifying the configuration file for font size adjustments according to system settings.

Example of configuration tag:

```json
{
  "app": {
    "configuration": "$profile:configuration"  
  }
}
```

The configuration file configuration.json is defined under AppScope/resources/base/profile in the development view. The filename "configuration" can be customized but must match the information specified in the configuration tag. The file lists the properties for font size adjustments according to system changes.

**Table 4** Description of configuration Tag

| Attribute Name | Description | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| fontSizeScale | Indicates whether the application font size follows the system. Supported values are:<br/>- followSystem: Follows the system.<br/>- nonFollowSystem: Does not follow the system.| String | This tag is optional, with a default value of "nonFollowSystem". |
| fontSizeMaxScale | The maximum ratio of the application font size to the system font size when following the system. Supported values are: 1, 1.15, 1.3, 1.45, 1.75, 2, 3.2.<br/>For example, if the maximum ratio is set to 1.75 and the default system font size is 10fp:<br/>(1) If the system font size is adjusted to 1.5x in settings, the actual system font size becomes 15fp, and the application font size will adjust to 15fp.<br/>(2) If the system font size is adjusted to 2x, the system font size becomes 20fp, but since the maximum ratio is 1.75, the application font size will be 17.5fp.<br/>**Note**<br/>This property does not apply if fontSizeScale is "nonFollowSystem". | String | This tag is optional, with a default value of "3.2". |

Example of configuration tag:

```json
{
  "configuration": {
    "fontSizeScale": "followSystem",
    "fontSizeMaxScale": "3.2"
  }
}
```