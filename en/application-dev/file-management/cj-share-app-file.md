# Application File Sharing

Application file sharing refers to the process where applications share files through URIs (Uniform Resource Identifier).

## File Sharing via Launching File Handler Applications (startAbility)

Based on the [File Picker (startAbility)](../application-models/cj-file-processing-apps-startup.md) sharing method, applications can share individual files. The receiving application can open the URI using [ohos.file_fs's open](../../../en/application-dev/reference/CoreFileKit/cj-apis-file_fs.md#static-func-openstring-int64) and perform read/write operations.

## Shareable Application Directories

| Sandbox Path                         | Description |
| -------                              | ---- |
| /data/storage/el1/base               | Application el1-level encrypted data directory |
| /data/storage/el2/base               | Application el2-level encrypted data directory |
| /data/storage/el2/distributedfiles   | Application el2 encrypted-level account-distributed data fusion directory |

## File URI Specification

The format of a file URI:

file://&lt;bundleName&gt;/&lt;path&gt;

- file: The identifier for a file URI.

- bundleName: The owner of the file resource.

- path: The path of the file resource within the application sandbox.