# Pushing Files to Application Sandbox  

During application development and debugging, developers may need to push certain files into the application sandbox for access or testing within the app. There are two approaches to achieve this:  

1. **Using DevEco Studio**: Files can be placed into the application installation path via DevEco Studio. For details, refer to [Application Installation Resource Access](..//cj-start/start/ide-resource-categories-and-access.md#资源访问).  

2. **Using the hdc Tool**: When a device environment is available, a more flexible method is to use the hdc tool to push files to the application sandbox path on the device. This document focuses on this approach.  

However, the file paths observed under the debugging process via `hdc shell` differ from the application sandbox paths from the app's perspective. Developers should first understand the [Mapping Between Application Sandbox Paths and Actual Physical Paths](./cj-app-sandbox-directory.md#应用沙箱路径和真实物理路径的对应关系).  

## Development Example  

Take the application package `com.ohos.example` as an example. If reading or writing files in the application sandbox path `/data/storage/el1/bundle`, the [Mapping Between Application Sandbox Paths and Actual Physical Paths](./cj-app-sandbox-directory.md#应用沙箱路径和真实物理路径的对应关系) document reveals that the corresponding actual physical path is `/data/app/el1/bundle/public/<PACKAGENAME>`, i.e., `/data/app/el1/bundle/public/com.ohos.example`.  

The file push command is as follows:  

```shell  
hdc file send ${local_path_of_file_to_push} /data/app/el1/bundle/public/com.ohos.example/  
```  

After pushing the file, set the file's `user_id` and `group_id` to the application's `user_id`. The application's `user_id` can be queried using the following command, where the first column of the process line is the application process's `user_id`:  

```shell  
hdc shell ps -ef | grep com.ohos.example  
```  

Use the application process's `user_id` to set the file's `user_id` and `group_id` with the following command:  

```shell  
hdc shell chown ${user_id}:${user_id} ${file_path}  
```  

## Switching to Application Sandbox Perspective  

During debugging, if permission issues or missing files occur, developers need to switch from the debugging process perspective to the application perspective for intuitive analysis of permissions and directory issues. The perspective switch commands are as follows:  

```shell  
hdc shell                         // Enter shell  
ps -ef|grep [hapName]             // Find the corresponding application's pid using the ps command  
nsenter -t [hapPid] -m /bin/sh    // Enter the application's sandbox environment using the pid found in the previous step  
```  

After execution, the perspective switches to the application sandbox view, where directory paths are the application sandbox paths, allowing developers to troubleshoot sandbox path-related issues.