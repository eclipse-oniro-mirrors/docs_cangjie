# ATM Tool  

Access Token Manager (referred to as the ATM tool) is a utility for querying <!--Del-->or setting<!--DelEnd--> application process permissions, usage types, and related information. It provides developers with the capability to manage access control based on token IDs, package names, process names, and other identifiers.

## Environment Setup  

Before using this tool, developers need to obtain the [hdc tool](./cj-hdc.md) and execute `hdc shell`.  

## ATM Tool Command List  

| Command | Description |
| ------- | ----------- |
| help    | Help command, displays supported ATM commands. |
| <!--DelRow-->perm   | Permission command, grants or revokes permissions for application processes. |
| <!--DelRow-->toggle | Popup toggle/permission usage log toggle command, sets or retrieves the status of permission popups/permission usage logs. This command is only available in root versions. |
| dump    | Query command, retrieves access control-related data. |

## Help Command  

```bash
# Display help information  
atm help  
```  

<!--Del-->  

## Permission Command  

```bash  
atm perm [-h] [-g -i <token-id> -p <permission-name>] [-c -i <token-id> -p <permission-name>]  
```  

**Permission Command Parameter List**  

| Parameter | Description |  
| :-------- | :---------- |  
| -h | Help information. Lists supported commands for `atm perm`. |  
| -g&nbsp;-i \<token-id>&nbsp;-p \<permission-name> | Mandatory parameters. Grants the specified permission to an application process using its token ID. Returns success status. |  
| -c&nbsp;-i \<token-id>&nbsp;-p \<permission-name> | Mandatory parameters. Revokes the specified permission from an application process using its token ID. Returns success status. |  

Example:  

```bash  
# Display help information for `atm perm`  
atm perm -h  

# Grant camera permission to an application process  
atm perm -g -i ********* -p ohos.permission.CAMERA  

# Revoke camera permission from an application process  
atm perm -c -i ********* -p ohos.permission.CAMERA  
```  

## Popup Toggle Status Command  

```bash  
atm toggle [-h] [-r -s -i <user-id> -p <permission-name> -k <status>] [-r -o -i <user-id> -p <permission-name>]  
```  

**Popup Toggle Status Command Parameter List**  

| Parameter | Description |  
| :-------- | :---------- |  
| -h | Help information. |  
| -r&nbsp;-s&nbsp;-i \<user-id>&nbsp;-p \<permission-name>&nbsp;-k \<status> | Mandatory parameters. Sets the popup toggle status for a specified permission under a given user ID. Returns success status. |  
| -r&nbsp;-o&nbsp;-i \<user-id>&nbsp;-p \<permission-name> | Mandatory parameters. Retrieves the popup toggle status for a specified permission under a given user ID. |  

Example:  

```bash  
# Display help information for `atm toggle`  
atm toggle -h  

# Enable popup toggle for camera permission under user 0  
atm toggle -r -s -i 0 -p ohos.permission.CAMERA -k 1  

# Retrieve popup toggle status for camera permission under user 0  
atm toggle -r -o -i 0 -p ohos.permission.CAMERA  
```  

## Permission Usage Log Toggle Status Command  

```bash  
atm toggle [-h] [-u -s -i <user-id> -k <status>] [-u -o -i <user-id>]  
```  

**Permission Usage Log Toggle Status Command Parameter List**  

| Parameter | Description |  
| :-------- | :---------- |  
| -h | Help information. |  
| -u&nbsp;-s&nbsp;-i \<user-id>&nbsp;-k \<status> | Mandatory parameters. Sets the permission usage log toggle status under a given user ID. Returns success status. |  
| -u&nbsp;-o&nbsp;-i \<user-id> | Mandatory parameters. Retrieves the permission usage log toggle status under a given user ID. |  

Example:  

```bash  
# Display help information for `atm toggle`  
atm toggle -h  

# Enable permission usage log toggle for user 0  
atm toggle -u -s -i 0 -k 1  

# Retrieve permission usage log toggle status for user 0  
atm toggle -u -o -i 0  
```  

<!--DelEnd-->  

## Query Command  

<!--RP1-->  

```bash  
atm dump [-h] [-t [-i <token-id>] [-b <bundle-name>] [-n <process-name>]] [-r [-i <token-id>] [-p <permission-name>]] [-v [-i <token-id>] [-p <permission-name>]]  
```  

<!--RP1End-->  

In the commands listed below, `-t`, <!--Del-->`-r`, <!--DelEnd-->`-v` are mandatory parameters, while `-i`, `-b`, `-n`, `-p` are optional. For `atm dump -v`, `-i` and `-p` can be combined; for <!--Del-->`atm dump -r` and <!--DelEnd-->`atm dump -v`, `-i` and `-p` can be combined; for `atm dump -t`, `-i`, `-b`, `-n` can only be used individually.  

| Parameter | Description |  
| ----- | ----- |  
| -h | Help information. |  
| -t | Mandatory parameter. Queries all application process information in the system. |  
| -t&nbsp;-i \<token-id> | Optional parameter. Queries basic information and corresponding [permission information](../../../en/application-dev/reference/AbilityKit/cj-apis-ability_access_ctrl.md#enum-grantstatus) for an application process using its token ID. |  
| -t&nbsp;-b \<bundle-name> | Optional parameter. Queries basic information and corresponding [permission information](../../../en/application-dev/reference/AbilityKit/cj-apis-ability_access_ctrl.md#enum-grantstatus) for an application process using its bundle name. |  
| -t&nbsp;-n \<process-name> | Optional parameter. Queries basic information and corresponding [permission information](../../../en/application-dev/reference/AbilityKit/cj-apis-ability_access_ctrl.md#enum-grantstatus) for an application process using its process name. |  
| <!--DelRow-->-r | Mandatory parameter. Queries all permission usage logs in the system. |  
| <!--DelRow-->-r&nbsp;-i \<token-id> | Optional parameter. Queries permission usage logs for an application process using its token ID. |  
| <!--DelRow-->-r&nbsp;-p \<permission-name> | Optional parameter. Queries usage logs for a specified permission. |  
| -v | Mandatory parameter. Queries permission usage types for all application processes in the system. |  
| -v&nbsp;-i \<token-id> | Optional parameter. Queries permission usage types for an application process using its token ID. |  
| -v&nbsp;-p \<permission-name> | Optional parameter. Queries usage types for a specified permission. |  

Example:  

```bash  
# Query all permission definitions in the system  
atm dump -d  

# Query permission definition by permission name  
atm dump -d -p *********  
# Execution result  
# {  
#     "permissionName": "ohos.permission.KERNEL_ATM_SELF_USE",  
#     "grantMode": SYSTEM_GRANT,  
#     "availableLevel": SYSTEM_CORE,  
#     "availableType": SYSTEM,  
#     "provisionEnable": true,  
#     "distributedSceneEnable": true,  
#     "isKernelEffect": true,  
#     "hasValue": true,  
# }  

# Display help information for `atm dump`  
atm dump -h  

# Query token IDs and bundle names for all application processes in the system  
atm dump -t  

# Query permission information by token ID  
atm dump -t -i *********  
# Execution result  
# {  
#   "tokenID": 672078897,  
#   "processName": "samgr",  
#   "apl": 2,  
#   "permStateList": [  
#     {  
#       "permissionName": "ohos.permission.DISTRIBUTED_DATASYNC",  
#       "grantStatus": 0,  
#       "grantFlag": 4,  
#     }  
#   ]  
# }  

# Query permission information by bundle name  
atm dump -t -b ohos.telephony.resources  
# Execution result  
# {  
#   "tokenID": 537280686,  
#   "tokenAttr": 1,  
#   "ver": 1,  
#   "userId": 100,  
#   "bundleName": "ohos.telephony.resources",  
#   "instIndex": 0,  
#   "dlpType": 0,  
#   "isRemote": 0,  
#   "isPermDialogForbidden": 0,  
#   "permStateList": [  
#     {  
#       "permissionName": "ohos.permission.DISTRIBUTED_DATASYNC",  
#       "grantStatus": 0,  
#       "grantFlag": 4,  
#     }  
#   ]  
# }  

# Query permission information by process name  
atm dump -t -n *********  

# Query permission usage types for all applications  
atm dump -v  
# Execution result  
# {  
#   "tokenId": 537088946,  
#   "permissionName": ohos.permission.GET_INSTALLED_BUNDLE_LIST,  
#   "usedType": 0,  
# }  

# Query permission usage types by application token ID  
atm dump -v -i *********  

# Query permission usage types by permission name  
atm dump -v -p ohos.permission.CAMERA  

# Query permission usage types by application token ID and permission name  
atm dump -v -i ********* -p ohos.permission.CAMERA  
```  

<!--Del-->  

```bash  
# Query all permission usage logs in the system  
atm dump -r  
# Execution result  
# {  
#   "beginTime": 1501837281916,  
#   "endTime": 1501837281916,  
#   "bundleRecords": [  
#     {  
#       "tokenId": 537088946,  
#       "isRemote": 0,  
#       "bundleName": com.ohos.permissionmanager,  
#       "permissionRecords": [  
#         {  
#           "permissionName": "ohos.permission.GET_INSTALLED_BUNDLE_LIST",  
#           "accessCount": "1",  
#           "secAccessCount": "0",  
#           "rejectCount": 0,  
#           "lastAccessTime": 1501837281916,  
#           "lastRejectTime": 0,  
#           "lastAccessDuration": 0,  
#           "accessRecords": [  
#             {  
#               "status": "1",  
#               "lockScreenStatus": "1",  
#               "timestamp": "1501837281916",  
#               "duration": 0,  
#               "count": 1,  
#               "usedType": 0,  
#             },  
#           ]  
#           "rejectRecords": [  
#           ]  
#         },  
#       ]  
#     }  
#   ]  
# }  

# Query permission usage logs by application token ID  
atm dump -r -i *********  

# Query permission usage logs by permission name  
atm dump -r -p ohos.permission.CAMERA  

# Query permission usage logs by application token ID and permission name  
atm dump -r -i ********* -p ohos.permission.CAMERA  
```  

<!--DelEnd-->