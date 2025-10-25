# Application/Component-Level Configuration

When developing an application, certain tags need to be configured, such as the application's package name, icon, and other identifying attributes. This document describes key tags that require configuration during application development.

## Application Package Name Configuration

The application must configure the `bundleName` tag in the [app.json5 configuration file](../cj-start/basic-knowledge/app-configuration-file.md) located in the AppScope directory of the project. This tag uniquely identifies the application. A reverse-domain naming convention is recommended (e.g., `com.example.demo`, where the first level is the domain suffix `com`, the second level is the vendor/personal name, and the third level is the application name; additional levels are also acceptable).

## Icon and Label Configuration

Icons and labels are typically configured together, corresponding to the `icon` and `label` fields in the [app.json5 configuration file](../cj-start/basic-knowledge/app-configuration-file.md) and [module.json5 configuration file](../cj-start/basic-knowledge/module-configuration-file.md). Starting from DevEco Studio 5.0.3.800, the `icon` and `label` fields in the [module.json5 configuration file](../cj-start/basic-knowledge/module-configuration-file.md) are no longer mandatory, while they remain required in the [app.json5 configuration file](../cj-start/basic-knowledge/app-configuration-file.md). Therefore, the `icon` and `label` fields in the [module.json5 configuration file](../cj-start/basic-knowledge/module-configuration-file.md) can be omitted.

### Generation Mechanism

* **HAP contains UIAbility**:
    * If the `icon` and `label` are configured in the `abilities` tag of the module.json5 configuration file, and the corresponding ability's `skills` tag includes `"entity.system.home"` in `entities` and `"ohos.want.action.home"` or `"action.system.home"` in `actions`, the system will prioritize the `icon` and `label` from module.json5. If multiple qualifying abilities exist, the system will prioritize the `icon` and `label` configured for the ability specified in `mainElement` of module.json5.
    * If the `icon` and `label` are not set in the `abilities` tag of module.json5, the system will use the `icon` and `label` from app.json5.
* **HAP does not contain UIAbility**: The system will use the `icon` and `label` from app.json5.

### Application Scenarios

<!--RP1-->

* **Displaying the current application in the application interface**: For example, showing the application list in the Settings app or displaying permissions requested by the app in the Privacy Management section.
* **Displaying the current application on the device desktop**: For example, showing the app on the home screen or in the recent tasks list.

<!--RP1End-->

The effect is illustrated below:
<!--RP2-->
![application-component-configuration-stage-app-module](./figures/application-component-configuration-stage-app-module.png)
<!--RP2End-->

### Configuration Examples

* **Method 1: Configure app.json5 (Recommended)**

  ```json
  {
    "app": {
      "icon": "$media:app_icon",
      "label": "$string:app_name"
      // ...
    }
  }
  ```

* **Method 2: Configure module.json5**

  To display the UIAbility icon on the desktop, in addition to configuring the `icon` and `label` fields, you must also add `"entity.system.home"` to `entities` and `"ohos.want.action.home"` to `actions` under the `skills` tag.

  ```json
  {
    "module": {
      // ...
      "abilities": [
        {
          "icon": "$media:icon",
          "label": "$string:EntryAbility_label",
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
        }
      ]
    }
  }
  ```

### Control Rules

The system enforces strict controls on applications without icons to prevent malicious apps from intentionally hiding their desktop icons, which could make it difficult for users to locate and uninstall the software, thereby ensuring device security to some extent.

If a pre-installed application requires hiding its desktop icon, it must configure the `AllowAppDesktopIconHide` application privilege<!--Del-->. For specific configuration details, refer to the [Application Privilege Configuration Guide](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-app-privilege-config-guide.md)<!--DelEnd-->. After obtaining this privilege, the application will not appear on the desktop. Non-pre-installed applications are not allowed to hide their desktop icons.

## Application Version Declaration Configuration

The application version declaration requires configuring the `versionCode` and `versionName` tags in the [app.json5 configuration file](../cj-start/basic-knowledge/app-configuration-file.md) located in the AppScope directory. The `versionCode` identifies the application's version number as a 32-bit non-negative integer. This number is solely used to determine whether one version is newer than another, with higher values indicating newer versions. The `versionName` tag provides a textual description of the version number.

## Module-Supported Device Types Configuration

The device types supported by a Module must be configured in the [module.json5 configuration file](../cj-start/basic-knowledge/module-configuration-file.md) under the [deviceTypes tag](../cj-start/basic-knowledge/module-configuration-file.md#devicetypes标签). Adding a device type to this tag indicates that the current Module supports running on that device.

## Module Permission Configuration

Permissions required for a Module to access protected parts of the system or other applications must be configured in the [module.json5 configuration file](../cj-start/basic-knowledge/module-configuration-file.md) under the [requestPermissions tag](../security/AccessToken/cj-declare-permissions.md). This tag declares the permission name, the reason for requesting it, and the usage scenario.