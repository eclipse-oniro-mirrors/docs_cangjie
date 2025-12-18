# Pushing Files to Application Sandbox

During application development and debugging, developers may need to push certain files into the application sandbox for access or testing within the app. There are two approaches available:

1. Using DevEco Studio to place target files in the application installation path. For details, refer to [Application Installation Resource Access](..//cj-start/start/ide-resource-categories-and-access.md#resource-access).

2. When device environment is available, a more flexible alternative is using the hdc tool to push files to the application sandbox path on the device. This document focuses on this method.

Note that the file paths under debugging processes visible via hdc shell differ from the application sandbox paths from the app's perspective. Developers should first understand the [Correspondence Between Application Sandbox Paths and Actual Physical Paths](./cj-app-sandbox-directory.md#correspondence-between-application-sandbox-paths-and-actual-physical-paths).

## Development Example

Taking application package `com.ohos.example` as an example, if reading/writing files in the application sandbox path `/data/storage/el1/bundle`, the [Correspondence Between Application Sandbox Paths and Actual Physical Paths](./cj-app-sandbox-directory.md#correspondence-between-application-sandbox-paths-and-actual-physical-paths) document indicates the corresponding actual physical path is `/data/app/el1/bundle/public/<PACKAGENAME>`, specifically `/data/app/el1/bundle/public/com.ohos.example`.

Example push command:

```shell
hdc file send ${local_path_to_file} /data/app/el1/bundle/public/com.ohos.example/
```

After file transfer, set the file's user_id and group_id to match the application's user_id. Query the application's user_id using this command (the first column in the process line shows the application process user_id):

```shell
hdc shell ps -ef | grep com.ohos.example
```

Set the file's user_id and group_id using the application process's user_id:

```shell
hdc shell chown ${user_id}:${user_id} ${file_path}
```

## Switching to Application Sandbox Perspective

During debugging, if encountering permission issues or missing files, developers should switch from the debugging process perspective to the application perspective for direct analysis of permission and directory issues. Use these commands to switch perspectives:

```shell
hdc shell                         # Enter shell
ps -ef|grep [hapName]             # Find corresponding application pid via ps command
nsenter -t [hapPid] -m /bin/sh    # Enter application sandbox environment using the pid found above
```

After execution, you'll be in the application perspective where directory paths represent application sandbox paths, allowing investigation of sandbox path-related issues.