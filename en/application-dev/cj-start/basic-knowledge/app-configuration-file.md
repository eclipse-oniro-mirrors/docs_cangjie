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

**Table 1** app.json5 Configuration File Tag Descriptions

| Attribute Name | Description | Data Type | Optional |
| -------- |--------------------------| -------- | -------- |
| bundleName | Identifies the Bundle name of the application, used to ensure uniqueness. Naming rules are as follows:<br/>- Must be a dot-separated string with at least three segments, where each segment can only contain letters, numbers, and underscores (_).<br/>- The first segment must start with a letter, while non-first segments must start with a number or letter and end with a number or letter.<br/>- Consecutive dots (.) are not allowed.<br/>- Minimum length is 7 bytes, maximum length is 128 bytes.<br/>- Recommended to use reverse domain name notation (e.g., "com.example.demo", where the first level is a domain suffix like com, the second level is the vendor/personal name, and the third level is the application name; multiple levels are also acceptable).<br/>For applications compiled with system source code, it is recommended to name them in the format "com.ohos.demo", where "ohos" identifies system applications. | String | This tag is mandatory. |
| bundleType| Identifies the Bundle type of the application, used to distinguish between applications and atomic services. Supported values:<br/>- app: The current Bundle is an application.<br/>- atomicService: The current Bundle is an atomic service.<br/>- shared: The current Bundle is a shared library application (reserved field).<br/>- appService: The current Bundle is a system-level shared library application, for system applications only. | String| Optional, default value is app. |
| debug | Indicates whether the application is debuggable.<br/>- true: Debuggable, typically used during development.<br/>- false: Not debuggable, typically used for release. | Boolean | Generated during compilation by DevEco Studio. Optional, default value is false. |
| [icon](#icon-tag) | Identifies the [application icon](../../application-models/cj-application-component-configuration-stage.md), referencing the index of the icon resource file. | String | This tag is mandatory. |
| label | Identifies the [application name](../../application-models/cj-application-component-configuration-stage.md), referencing the index of a string resource, with a maximum length of 63 bytes. | String | This tag is mandatory. |
| description | Identifies the application's description, referencing a string resource index with a maximum length of 255 bytes. This field can be used to display application information, such as on the About page. | String | Optional, default value is empty. |
| vendor | Identifies the application developer, with a maximum length of 255 bytes. This field can display developer information, such as on the About page. | String | Optional, default value is empty. |
| versionCode | Identifies the application version number, a positive integer less than 2^31. This number is only used to determine if one version is newer than another; higher values indicate newer versions.<br/>Developers can set this to any positive integer but must ensure newer versions use larger values than older ones. | Number | This tag is mandatory. |
| versionName | Displays the application version number to users.<br/>A string of up to 127 bytes, consisting only of numbers and dots, recommended in the "A.B.C.D" format. The four segments represent:<br/>First segment: Major version (0–99), indicating significant changes or new features.<br/>Second segment: Minor version (0–99), indicating notable features or major bug fixes.<br/>Third segment: Feature version (0–99), indicating planned new features.<br/>Fourth segment: Patch version (0–999), indicating maintenance releases or bug fixes. | String | This tag is mandatory. |
| minCompatibleVersionCode | Identifies the minimum historical version the application is compatible with, used for cross-device coordination, data migration, and compatibility checks (reserved field, currently unused). Range: 0–2147483647. | Number | Optional, default value equals versionCode. |
| minAPIVersion | Identifies the minimum SDK API version required to run the application. Range: 0–2147483647. | Number | Automatically generated during compilation, corresponding to the compatibleSdkVersion tag in the project-level build-profile.json5 file. For compatibility details, see [Application Compatibility](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/app-compatibility). |
| targetAPIVersion | Identifies the target API version required to run the application. Range: 0–2147483647. | Number | Automatically generated during compilation, corresponding to the compileSdkVersion tag in the project-level build-profile.json5 file. For compatibility details, see [Application Compatibility](https://developer.huawei.com/consumer/cn/doc/harmonyos-releases/app-compatibility). |
| apiReleaseType | Identifies the type of target API version, represented as a string. Values: "CanaryN", "BetaN", or "Release", where N is a positive integer.<br/>- Canary: Limited release version.<br/>- Beta: Public Beta version.<br/>- Release: Public stable version. | String | Automatically generated during compilation based on the SDK's Stage. Manual configurations will be overwritten. |
| accessible | Indicates whether the application can access its installation directory (only for Stage model system and preinstalled applications).<br/>- true: Can access.<br/>- false: Cannot access. | Boolean | Optional, default value is false. |
| multiProjects | Indicates whether the project supports multi-project development.<br/>- true: Supports multi-project development. See [Multi-Project Build](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-multi-projects).<br/>- false: Does not support. | Boolean | Optional, default value is false. |
| asanEnabled | Indicates whether ASAN (Address Sanitizer) detection is enabled to help locate buffer overflow crashes.<br/>- true: Enabled.<br/>- false: Disabled. | Boolean | Optional, default value is false. |
| tablet | Specifies configurations for tablet devices, such as minAPIVersion.<br/>If configured, tablet devices will use these values instead of the common app.json5 settings. | Object | Optional; if omitted, tablet devices use common app.json5 settings. |
| default | Specifies configurations for default devices, such as minAPIVersion.<br/>If configured, default devices will use these values instead of the common app.json5 settings. | Object | Optional; if omitted, default devices use common app.json5 settings. |
| targetBundleName| Identifies the target application for the current package, following the same rules as bundleName. Applications with this field are overlay applications. | String | Optional, default value is empty. |
| targetPriority| Identifies the priority of the current application, range: 1–100. Only configurable if targetBundleName is set. | Number | Optional, default value is 1. |
| generateBuildHash | Indicates whether the build tool generates hash values for all HAPs in the application.<br/>When true, all HAPs will have hash values generated. During OTA updates, if versionCode remains unchanged, the system can determine whether an update is needed based on hash values.<br/>- true: Hash values generated.<br/>- false: No hash values generated.<br/>**Note:** Only effective for preinstalled applications. | Boolean | Optional, default value is false. |
| [appEnvironments](#appenvironments-tag) | Configures environment variables for the current module. | Object Array | Optional, default value is empty. |
| maxChildProcess | Identifies the maximum number of child processes the application can create, range: 0–512 (0 means unlimited). For multi-module applications, the entry module's configuration takes precedence. | Number | Optional; if omitted, the system default is used. |
| [multiAppMode](#multiappmode-tag) | Configures the multi-instance mode for the application. Only valid for entry or feature modules of applications with bundleType=app; for multi-module applications, the entry module's configuration takes precedence. | Object | Optional, default value is empty. |
| cloudFileSyncEnabled | Indicates whether cloud file synchronization is enabled for the application.<br/>- true: Enabled.<br/>- false: Disabled. | Boolean | Optional, default value is false. |
| [configuration](#configuration-tag) | Configures the application's ability to adjust font size according to system settings.<br/>This tag references a profile file resource that specifies the configuration for font size adjustments. | String | Optional; if omitted, font size does not follow system settings by default. |
| assetAccessGroups | Configures the Group ID for the application, which combines with the Developer ID to form group information.<br/>During HAP packaging, DevEco signs the group information using the developer certificate, where group information consists of Developer ID (assigned by the app market) + Group ID (configured by the developer).<br/>**Note:** Supported from API version 18. | String Array | Optional, default value is empty. |

## icon Tag

This tag identifies the [application icon](../../application-models/cj-application-component-configuration-stage.md) and references the layered icon configuration file.

Layered icon configuration steps:

1. Place foreground and background resources in the AppScope/resources/base/media directory or use the default resources stored there.

2. The media directory contains a layered icon configuration file (layered_image.json), which references the foreground and background resources. For details, see [Icon Resource Specifications](https://developer.huawei.com/consumer/cn/doc/design-guides/application-icon-0000001953444009#section634668113212).

Layered icon configuration file example:

```json
{
  "layered-image":
    {
      "background":"$media:background", // Background resource
      "foreground":"$media:foreground" // Foreground resource
    }
}
```

icon tag example:

```json
{
  "app":{
    "icon":"$media:layered_image"
  }
}
```

## appEnvironments Tag

This tag configures environment variables for the application. Sometimes, applications depend on third-party libraries that use custom environment variables. To avoid modifying these libraries, you can set custom environment variables in the project configuration file for runtime use.

**Table 2** appEnvironments Tag Descriptions

| Attribute Name | Description | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| name | Identifies the environment variable name, with a maximum length of 4096 bytes. | String | Optional, default value is empty. |
| value | Identifies the environment variable value, with a maximum length of 4096 bytes. | String | Optional, default value is empty. |

appEnvironments tag example:

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

Configures the multi-instance mode for the application.

**Table 3** multiAppMode Tag Descriptions

| Attribute Name | Description | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| multiAppModeType | Identifies the multi-instance mode type. Supported values:<br/>- multiInstance: Multi-instance mode (only supported on 2-in-1 devices; not supported for resident processes).<br/>- appClone: Application clone mode. | String | This tag is mandatory. |
| maxCount | Identifies the maximum number of allowed instances. Supported ranges:<br/>- multiInstance mode: 1–10.<br/>- appClone mode: 1–5. | Number | This tag is mandatory. |

multiAppMode tag example:

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

This tag references a profile file resource that specifies the configuration for font size adjustments according to system settings.

configuration tag example:

```json
{
  "app": {
    "configuration": "$profile:configuration"  
  }
}
```

Define the configuration file configuration.json in the AppScope/resources/base/profile directory (the filename can be customized but must match the configuration tag). The file lists properties for font size adjustments.

**Table 4** configuration Tag Descriptions

| Attribute Name | Description | Data Type | Optional |
| -------- | -------- | -------- | -------- |
| fontSizeScale | Indicates whether the application font size follows the system. Supported values:<br/>- followSystem: Follows system settings.<br/>- nonFollowSystem: Does not follow system settings. | String | Optional, default value is nonFollowSystem. |
| fontSizeMaxScale | When fontSizeScale is followSystem, this specifies the maximum scaling ratio relative to the system font size. Supported values: 1, 1.15, 1.3, 1.45, 1.75, 2, 3.2.<br/>Example: If the maximum ratio is 1.75 and the default system font size is 10fp:<br/>(1) If the system adjusts to 1.5x, the actual font size becomes 15fp, and the application adjusts to 15fp.<br/>(2) If the system adjusts to 2x, the font size becomes 20fp, but the application caps at 17.5fp (1.75x).<br/>**Note:** Not effective when fontSizeScale is nonFollowSystem. | String | Optional, default value is 3.2. |

configuration tag example:

```json
{
  "configuration": {
    "fontSizeScale": "followSystem",
    "fontSizeMaxScale": "3.2"
  }
}
```