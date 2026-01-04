# Launching File Handling Applications (startAbility)

## Usage Scenario

For example, when an application downloads a PDF file in a browser, this interface can be called to select a file handling application to open the PDF file. Developers need to set fields such as the URI path of the file to be opened ([uri](#Key Parameter Descriptions)) and the file format ([type](#Key Parameter Descriptions)) in the request, so that the system can recognize and directly launch the file opening application or display a selection dialog for the user to choose an appropriate application to open the file. The effect is illustrated in the following figure.

Figure 1 Illustration of the Effect

![file-open](figures/file-open.jpeg)

## Key Parameter Descriptions

Developers can achieve opening files by installed vertical domain applications by calling the [startAbility](../reference/AbilityKit/cj-apis-app-ability.md#func-startabilitywant) interface.

**Table 1** Description of [Want](../reference/AbilityKit/cj-apis-app-ability.md#class-want) related parameters in the startAbility request

| Parameter Name | Type   | Required | Description       |
|----------------|--------|----------|------------------|
| uri            | String | Yes      | Indicates the URI path of the file to be opened, typically used in conjunction with type.<br/>URI format: file:\/\/bundleName\/path<br/>- file: Identifier for the file URI.<br/>- bundleName: The owner of the file resource.<br/>- path: The path of the file resource within the application sandbox. |
| type           | String | No       | Indicates the type of file to be opened. It is recommended to use [UTD types](../../database/cj-uniform-data-type-descriptors.md), such as: 'general.plain-text', 'general.image'. Currently, it is also compatible with [MIME type](https://www.iana.org/assignments/media-types/media-types.xhtml?utm_source=ld246.com), such as: 'text/xml', 'image/*', etc.<br/>**Note:** <br/>1. type is an optional field. If type is not provided, the system will attempt to determine the file type based on the URI suffix for matching. If type is provided, it must match the file type of the URI; otherwise, it may fail to match the appropriate application. The mapping between file suffixes and file types can be found in the [Uniform Type Descriptor (UTD) Preset List](../../database/cj-uniform-data-type-list.md).<br/>2. Passing \*/\* is not supported.|
| parameters     | String | No       | Indicates custom parameters defined by the system and assigned by developers as needed. For file opening scenarios, refer to Table 2.                                                                                                                                                                                       |
| flags          | UInt32 | No       | Indicates the handling method. For file opening scenarios, refer to Table 3.                                                                                                                                                                                       |

**Table 2** Description of [parameters](../reference/AbilityKit/cj-apis-app-ability.md#enum-params) related parameters

| Parameter Name                              | Type    | Description                                                                                                                                                                |
|---------------------------------------------|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ability.params.stream                       | String  | Indicates that the file URI carried should be authorized to the target party, used for scenarios where the file to be opened depends on other files. For example, opening a local HTML file that depends on other local resource files. The corresponding value must be a string array of file URIs. The file URI can be obtained by referring to the uri parameter in Table 1. |
| ohos.ability.params.showDefaultPicker       | Bool    | Indicates whether to forcibly display the file opening method selection dialog. The default is false.<br/>- false: The system policy or default application settings determine whether to directly launch the file opening application or display the dialog.<br/>- true: Always display the dialog.                                                                            |
| showCaller                                  | Bool    | Indicates whether the caller itself should participate in the matching as one of the target applications. The default is false.<br/>- false: Does not participate in matching.<br/>- true: Participates in matching.                                                                            |

**Table 3** Description of [flags](../reference/AbilityKit/cj-apis-app-ability.md#enum-flags) related parameters

| Parameter Name                       | Value         | Description                       |
|--------------------------------------|---------------|-----------------------------------|
| FlagAuthReadUriPermission            | 0x00000001    | Authorization to perform read operations on the URI. |
| FlagAuthWriteUriPermission           | 0x00000002    | Authorization to perform write operations on the URI. |

## Integration Steps

### Caller Integration Steps

1. Import relevant modules.

    <!-- compile -->

    ```cangjie

    import kit.AbilityKit.{UIAbility, Want, LaunchParam, Flags, WantValueType}
    import kit.ArkUI.WindowStage
    import kit.CoreFileKit.FileUri
    import ohos.business_exception.BusinessException
    import std.collection.HashMap
    ```

2. Obtain the application file path.

    <!-- compile -->

    ```cangjie

    // Assume the application bundleName is com.example.demo
    class MainAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
            // Obtain the file sandbox path
            let filePath = this
            .context
            .filesDir + '/test1.txt'
            // Convert the sandbox path to a URI
            let uri = FileUri(filePath).toString()
            // The obtained URI is "file://com.example.demo/data/storage/el2/base/files/test.txt"
        }
        // ...
    }
    ```

3. Construct the request data.

    <!-- compile -->

    ```cangjie

    // Assume the application bundleName is com.example.demo
    class MainAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
            // Obtain the file sandbox path
            let filePath = this
            .context
            .filesDir + '/test1.txt'
            // Convert the sandbox path to a URI
            let uri = FileUri(filePath).toString()
            // Construct the request data
            let want = Want(
                deviceId: "",
                bundleName: "",
                abilityName: "",
                moduleName: "",
                // Configure read/write permissions for the shared file, e.g., authorize the file opening application for read/write operations
                flags: Flags.FlagAuthWriteUriPermission.getValue() | Flags.FlagAuthReadUriPermission.getValue(),
                uri: uri,
                action: "ohos.want.action.viewData", // Indicates the action to view data, fixed to this value for file opening scenarios
                entities: [],
                dataType: 'general.plain-text', // Indicates the type of file to be opened
                parameters: HashMap<String, WantValueType>(),
                fds: HashMap<String, Int32>()
            )
        }
        // ...
    }
    ```

4. Call the interface to launch.

    <!-- compile -->

    ```cangjie

    class MainAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
            Hilog.info(1, "info", "MainAbility onWindowStageCreate.")
            // Obtain the file sandbox path
            let filePath = this
                .context
                .filesDir + '/test1.txt'
            // Convert the sandbox path to a URI
            let uri = FileUri(filePath).toString()
            // The obtained URI is "file://com.example.demo/data/storage/el2/base/files/test1.txt"
            // Construct the request data
            let want = Want(
                deviceId: "",
                bundleName: "",
                abilityName: "",
                moduleName: "",
                // Configure read/write permissions for the shared file, e.g., authorize the file opening application for read/write operations
                flags: Flags.FlagAuthWriteUriPermission.getValue() | Flags.FlagAuthReadUriPermission.getValue(),
                uri: uri,
                action: "ohos.want.action.viewData", // Indicates the action to view data, fixed to this value for file opening scenarios
                entities: [],
                dataType: 'general.plain-text', // Indicates the type of file to be opened
                parameters: HashMap<String, WantValueType>(),
                fds: HashMap<String, Int32>()
            )
            try {
                this
                    .context
                    .startAbility(want)
            } catch (e: BusinessException) {
                Hilog.error(1, "info", "Failed to invoke startAbility, code: ${e.code}, message: ${e.message}")
            }
        }
    }
    ```

### Target Party Integration Steps

1. Declare file opening capability.

    Applications that support opening files need to declare the file opening capability in the [module.json5](../cj-start/basic-knowledge/module-configuration-file.md) configuration file. The uris field indicates the type of URI to be received, where the scheme is fixed as file. The type field indicates the supported file types for opening (refer to [MIME type](https://www.iana.org/assignments/media-types/media-types.xhtml?utm_source=ld246.com)). In the following example, the type is a txt file.

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
                "ohos.want.action.viewData" // Required, declares data handling capability
                ],
                "uris": [
                {
                    // Allows opening local files identified by the file:// protocol in the URI
                    "scheme": "file", // Required, declares the protocol type as file
                    "type": "general.plain-text", // Required, indicates the supported file type for opening
                    "linkFeature": "FileOpen" // Required and case-sensitive, indicates that the URI's function is file opening
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

2. Application processes the file to be opened.

    <!-- compile -->

    ```cangjie

    import kit.AbilityKit.{UIAbility, Want, LaunchParam}
    import kit.ArkUI.{WindowStage}
    import kit.CoreFileKit.{FileIo, OpenMode}
    import kit.ArkUI.BusinessException

    class MainAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            // Obtain the uri field from the want information
            let uri = want.uri
            if (uri == "") {
                Hilog.error(1, "info", 'uri is invalid')
                return
            }
            try {
                // Perform corresponding operations based on the URI of the file to be opened. For example, open the URI in read-write mode to obtain the file object
                let file = FileIo.open(uri, mode: OpenMode.READ_WRITE)
                Hilog.info(1, "info", "Succeed to open file.")
            } catch (e: BusinessException) {
                Hilog.error(1, "info", "Failed to open file openSync, code: ${e.code}, message: ${e.message}")
            }
        }
    }
    ```