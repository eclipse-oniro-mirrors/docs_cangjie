# restool Tool

## Introduction

restool is an application engineering resource compilation tool that creates resource indexes and parses resources by compiling resource files. Developers can access corresponding resources by calling the [Resource Management Interface](../../../en/application-dev/reference/LocalizationKit/cj-apis-resource_manager.md). The restool tool is located in the toolchains subdirectory of the SDK installation directory.

## Parameter Description

restool currently supports the following command options:

| Option | Optional | Has Parameter | Description |
| -------- | -------- | -------- | -------- |
| -i | Required | With parameter | Specifies the resource directory to be built or the resource middleware to be built. Can be specified multiple times in the same command.<br>Refer to [Compile Resource Command](#compile-resources) for details. |
| -j | Required | With parameter | Specifies the path to the config.json or module.json file. |
| -o | Required | With parameter | Specifies the output path for compiled resources. |
| -p | Required | With parameter | Specifies the bundle name for compiled resources. |
| -r | Required | With parameter | Specifies the header file path for resources, with three formats: ".txt", ".js", or ".h". |
| -e | Optional | With parameter | Specifies the starting ID value for generated resources, e.g., 0x01000000, within ranges [0x01000000, 0x06FFFFFF) or [0x08000000, 0x41FFFFFF). |
| -f | Optional | Without parameter | If the output path already exists, forcibly delete and regenerate. |
| -h | Optional | Without parameter | Displays tool help information. |
| -m | Optional | With parameter | Specifies multiple module names for multi-module joint compilation, connected by ",". |
| -x | Optional | With parameter | Specifies the resource directory or single resource path for generating intermediate files. Can be specified multiple times in the same command. |
| -z | Optional | Without parameter | Generates compilation results for resource intermediate file directories. |
| -v | Optional | Without parameter | Displays the tool version number. |
| --ids | Optional | With parameter | Specifies the output directory for generating id_defined.json. |
| --defined-ids | Optional | With parameter | Specifies the path to the id_defined.json file, usually generated via --ids.<br>id_defined.json contains a list of resource types, names, and their IDs.<br>Developers can customize resource IDs in id_defined.json. |
| --icon-check | Optional | Without parameter | Enables PNG image validation for icons and startWindowIcon. |
| --target-config | Optional | With parameter | Used with the "-i" command to support selective compilation.<br>[Parameter Description](#target-config-parameter-description): Specifies configurations to include. |

### target-config Parameter Description

Supported configuration types: MccMnc, Locale, Orientation, Device, ColorMode, Density.

Parameter format: Configurations are separated by ";", and values within configurations are enclosed in "[]" and separated by ",".

MccMnc matching rules: Mcc (country code) must be the same; Mnc (network code) defaults to match if not present, otherwise Mnc must be the same.

Locale matching rules: Locale matching must satisfy the following three rules.

1. Language must be the same.
2. Script (writing system) defaults to match if not present, otherwise must be the same.
3. Country or region defaults to match if not present, otherwise must be the same.

    Example parameter: Locale[zh_CN,en_US];Device[phone]. This parameter filters other languages, retaining only zh_CN and en_US; filters other devices, retaining only phone; other parameters (e.g., MccMnc, Orientation) are not filtered and are retained.

## Usage Examples

For example, the entry directory structure is as follows:

```text
entry/src/main
|    |----resource
|    |    |----base
|    |    |    |----element
|    |    |    |----media
|    |    |    |----profile
|    |    |----rawfile
|    |    |----resfile
|    |----config.json/module.json
```

### Compile Resources

There are two ways to compile resources: full resource compilation and incremental resource compilation.

1. Full resource compilation command:

    ```bash
    restool -i entry/src/main -j entry/src/main/module.json -p com.ohos.demo -o out -r out/ResourceTable.txt -f
    ```

2. Incremental resource compilation steps:

    Step 1: Generate resource middleware with the following command:

    ```bash
    restool -x entry/src/main/resource -o out
    ```

    Step 2: Compile resource middleware with the following command:

    ```bash
    restool -i out1 -i out2 -o out -p com.ohos.demo -r out/ResourceTable.txt -j entry/src/main/module.json -f -z
    ```

### Fix Resource IDs

Steps to fix resource IDs:

Step 1: Create an id_defined.json file. There are two methods: via command line or custom.

- Method 1: Generate the file via command line:

```bash
restool -i entry/src/main -j entry/src/main/module.json -p com.ohos.demo -o out -r out/ResourceTable.txt --ids out -f
```

- Method 2: Custom file. The filename must be id_defined.json, with the following content:

```json
{
    "record" :
    [
        {
            "id" : "0x01000000", // The fixed ID value for the resource
            "name" : "app_name", // Resource name
            "type" : "string" // Resource type
        }
    ]
}
```

Step 2: Fix resource IDs. There are two ways to complete the fix: via Command 1 or by placing the custom id_defined.json in the resource/base/element/ directory and then using Command 2.

- Command 1:

```bash
restool -i entry/src/main -j entry/src/main/module.json -p com.ohos.demo -o out1 -r out1/ResourceTable.txt --defined-ids out/id_defined.json -f
```

- Command 2:

```bash
restool -i entry/src/main -j entry/src/main/module.json -p com.ohos.demo -o out1 -r out1/ResourceTable.txt -f
```