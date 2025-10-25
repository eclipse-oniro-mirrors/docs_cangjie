# Launching File Handler Applications (startAbility)

## Usage Scenario

For instance, when a browser application downloads a PDF file, this interface can be invoked to select a file handler application to open the PDF. Developers need to specify the URI path ([uri](#Key Parameter Specifications)) and file format ([type](#Key Parameter Specifications)) in the request, enabling the system to either directly launch a file-opening application or display a selection dialog for users to choose an appropriate application. The visual effect is illustrated below.

Figure 1 Visual Demonstration

![file-open](figures/file-open.jpeg)

## Key Parameter Specifications

## Implementation Steps

**Table 1** Description of [Want](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-want.md#class-want) Parameters in startAbility Requests

| Parameter Name | Type   | Required | Description                                                                                                                                                                                   |
|----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| uri            | String | Yes      | The URI path of the file to be opened, typically used in conjunction with `type`.<br/>URI format: `file://bundleName/path`<br/>- `file`: Identifier for file URIs.<br/>- `bundleName`: Owner of the file resource.<br/>- `path`: Path of the file resource within the application sandbox. |
| type           | String | No       | The type of file to be opened. Currently compatible with [MIME type](https://www.iana.org/assignments/media-types/media-types.xhtml?utm_source=ld246.com), e.g., `text/xml`, `image/*`, etc.<br/>**Note:** <br/>1. `type` is optional. If not provided, the system attempts to infer the file type from the URI suffix. If provided, ensure it matches the file type in the URI; otherwise, the system may fail to find a suitable application.<br/>2. `*/*` is not supported. |
| parameters     | String | No       | Custom parameters defined by the system and assigned by developers as needed. For file-opening scenarios, see Table 2.                                                                       |
| flags          | UInt32 | No       | Processing method. For file-opening scenarios, see Table 3.                                                                                                                                  |

**Table 2** Description of [parameters](../../../en/application-dev/reference/AbilityKit/cj-apis-ability.md#enum-params)  

| Parameter Name                              | Type    | Description                                                                                                                                                                |
|---------------------------------------------|---------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ability.params.stream                       | String  | Indicates that the file URI should be authorized to the target party, used when the file to be opened has dependencies on other files (e.g., local HTML files relying on local resource files). The value must be a string array of file URIs. File URI format follows the `uri` parameter in Table 1. |
| ohos.ability.params.showDefaultPicker       | Bool    | Whether to force-display a selection dialog for file-opening methods. Default is `false`.<br/>- `false`: The system decides whether to directly launch the file-opening app or display a dialog based on policies or default app settings.<br/>- `true`: Always display the dialog.                      |
| showCaller                                  | Bool    | Whether the caller itself should participate in the matching process as a target application. Default is `false`.<br/>- `false`: Does not participate.<br/>- `true`: Participates.                                                      |

**Table 3** Description of [flags](../../../en/application-dev/reference/AbilityKit/cj-apis-ability.md#enum-flags)  

| Parameter Name                       | Value       | Description                       |
|--------------------------------------|-------------|-----------------------------------|
| FlagAuthReadUriPermission        | 0x00000001  | Grants read permission for the URI. |
| FlagAuthWriteUriPermission       | 0x00000002  | Grants write permission for the URI. |

## Integration Steps

### Caller Integration Steps

1. Import relevant modules.

    <!-- compile -->

    ```cangjie

    import kit.AbilityKit.{UIAbility, Want, LaunchParam, Flags}
    import kit.ArkUI.WindowStage
    import kit.CoreFileKit.FileUri
    import ohos.business_exception.BusinessException
    ```

2. Obtain the application file path.

    <!-- compile -->

    ```cangjie

    // Assuming the application bundleName is com.example.demo
    class MainAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
            // Get the file sandbox path
            let filePath = this
            .context
            .filesDirectory + '/test1.txt'
            // Convert sandbox path to URI
            let uri = FileUri.getUriFromPath(filePath)
            // The obtained URI will be "file://com.example.demo/data/storage/el2/base/files/test.txt"
        }
        // ...
    }
    ```

3. Construct request data.

    <!-- compile -->

    ```cangjie

    // Assuming the application bundleName is com.example.demo
    class MainAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
            // Get the file sandbox path
            let filePath = this
            .context
            .filesDirectory + '/test1.txt'
            // Convert sandbox path to URI
            let uri = FileUri.getUriFromPath(filePath)
            // Construct request data
            let want = Want(
                action: "ohos.want.action.viewData", // Fixed value for file opening scenarios, indicating data viewing operation
                uri: uri,
                `type`: 'general.plain-text', // Specifies the file type to be opened
                // Configure read/write permissions for shared files, e.g., granting permissions to the file handler application
                flags: Flags.FlagAuthWriteUriPermission.getValue() | Flags.FlagAuthReadUriPermission.getValue()
            )
        }
        // ...
    }
    ```

4. Invoke the launch interface.

    <!-- compile -->

    ```cangjie

    class MainAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
            AppLog.info("MainAbility onWindowStageCreate.")
            // Get the file sandbox path
            let filePath = this
                .context
                .filesDirectory + '/test1.txt'
            // Convert sandbox path to URI
            let uri = FileUri.getUriFromPath(filePath)
            // The obtained URI will be "file://com.example.demo/data/storage/el2/base/files/test1.txt"
            // Construct request data
            let want = Want(
                action: "ohos.want.action.viewData", // Fixed value for file opening scenarios, indicating data viewing operation
                uri: uri,
                `type`: 'general.plain-text', // Specifies the file type to be opened
                // Configure read/write permissions for shared files, e.g., granting permissions to the file handler application
                flags: Flags.FlagAuthWriteUriPermission.getValue() | Flags.FlagAuthReadUriPermission.getValue()
            )
            try {
                this
                    .context
                    .startAbility(want)
            } catch (e: BusinessException) {
                AppLog.error("Failed to invoke startAbility, code: ${e.code}, message: ${e.message}")
            }
        }
    }
    ```

### Target Application Implementation Steps

1. Declare file handling capability.

    Applications supporting file opening must declare this capability in the [module.json5](../cj-start/basic-knowledge/module-configuration-file.md) configuration file. The `uris` field specifies supported URI types (with `scheme` fixed as `file`), while `type` indicates supported file formats (refer to [MIME type list](https://www.iana.org/assignments/media-types/media-types.xhtml?utm_source=ld246.com)). The example below demonstrates support for TXT files.

    ```json
    {
    "module": {
        // ...
        "abilities": [
        {
            // ...
            "skills": [
            {
                "actions": [
                "ohos.want.action.viewData" // Required: Declares data handling capability
                ],
                "uris": [
                {
                    // Allows opening local files with URI starting with file:// protocol
                    "scheme": "file", // Required: Declares file protocol type
                    "type": "general.plain-text", // Required: Specifies supported file type
                    "linkFeature": "FileOpen" // Required (case-sensitive): Indicates URI functionality for file opening
                }
                // ...
                ]
                // ...
            }
            ]
        }
        ]
    }
    }
    ```

2. Process target files.

    <!-- compile -->

    ```cangjie

    import kit.AbilityKit.{UIAbility, Want, LaunchParam}
    import kit.ArkUI.{WindowStage}
    import kit.CoreFileKit.{FileFs, OpenMode}
    import kit.ArkUI.BusinessException

    class MainAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            // Extract URI from want information
            let uri = want.uri
            if (uri == "") {
                AppLog.error('uri is invalid')
                return
            }
            try {
                // Perform operations based on the target file URI. Example: Open URI synchronously to obtain file object
                let file = FileFs.open(uri, mode: OpenMode
                    .READ_WRITE
                    .mode)
                AppLog.info("Succeed to open file.")
            } catch (e: BusinessException) {
                AppLog.error("Failed to open file openSync, code: ${e.code}, message: ${e.message}")
            }
        }
    }
    ```