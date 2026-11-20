# ohos.ability_access_ctrl (Application Access Control Management)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Application access control provides permission management capabilities for applications, including authentication, authorization, and revocation of authorization.

## Import Module

```cangjie
import kit.AbilityKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample project and configuration template, please refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class AbilityAccessCtrl

```cangjie
public class AbilityAccessCtrl {}
```

**Description:** This class is used to create [AtManager](#class-atmanager), which is an instance of the program access control management class.

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 22

### static func createAtManager()

```cangjie
public static func createAtManager(): AtManager
```

**Description:** Creates a program access control management instance for scenarios such as permission verification and runtime permission request. After the call is successful, an [AtManager](#class-atmanager) instance is returned, which can be used for subsequent permission management operations.

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| [AtManager](#class-atmanager) | **AtManager** instance obtained. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.AbilityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let atManager: AtManager = AbilityAccessCtrl.createAtManager()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class AtManager

```cangjie
public class AtManager {}
```

**Description:** Program access control management class, providing capabilities such as permission verification and runtime permission dialog box request. Obtain an instance through [createAtManager](#static-func-createatmanager).

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 22

### func checkAccessToken(UInt32, Permissions)

```cangjie
public func checkAccessToken(tokenID: UInt32, permissionName: Permissions): GrantStatus
```

**Description:** Verifies whether an app has been granted the specified permission. After the call is successful, the authorization status of the current permission is returned. The developer can decide accordingly whether to directly execute subsequent services or continue to initiate a permission request.

Applicable to scenarios where a pre-permission check is performed before an app accesses protected resources such as the camera, microphone, or location.

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| tokenID | UInt32 | Yes | - | Identity identifier of the target application to be verified. Can be obtained through the accessTokenId field of the application's [ApplicationInfo](cj-apis-bundle_manager.md#class-applicationinfo). This parameter must be an integer greater than 0. Passing in 0 throws error code 12100001. |
| permissionName | [Permissions](#type-permissions) | Yes | - | Name of the permission to be verified. The permission name cannot exceed 256 characters. Passing in an invalid value throws error code 12100001. Valid permission names can be queried in the [Application Permission List](../../security/AccessToken/cj-app-permissions.md). |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [GrantStatus](#enum-grantstatus) | Returns the authorization status result. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Access Control Error Codes](./cj-errorcode-access-token.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 12100001 | Invalid parameter. The tokenID is 0, or the permissionName exceeds 256 characters. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.AbilityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let atManager = AbilityAccessCtrl.createAtManager()
    let tokenID : UInt32 = 1 // tokenID can be obtained by system applications through bundleManager.getApplicationInfo, and by regular applications through bundleManager.getBundleInfoForSelf
    let status = atManager.checkAccessToken(tokenID, "ohos.permission.READ_CONTACTS")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func requestPermissionsFromUser(UIAbilityContext, Array\<Permissions>, AsyncCallback\<PermissionRequestResult>)

```cangjie
public func requestPermissionsFromUser(context: UIAbilityContext, permissionList: Array<Permissions>,
    requestCallback: AsyncCallback<PermissionRequestResult>): Unit
```

**Description:** Used by UIAbility to bring up a dialog box to request user authorization, and returns the authorization result of the permissions requested this time. This API uses an asynchronous callback to return the result.

Applicable to scenarios where an app proactively applies for permissions from the user before accessing protected resources for the first time.

If the user denies authorization, the authorization dialog box cannot be brought up again through this API. The developer can guide the user to go to the system settings interface for manual authorization.

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Context of the <!--RP1-->UIAbility<!--RP1End--> requesting the permission. If the context of another app or an invalid page is passed in, the API may report an error or fail to display the dialog box. |
| permissionList | Array\<[Permissions](#type-permissions)> | Yes | - | List of permission names. This array cannot be empty. It is recommended to pass in only the sensitive permissions necessary for the current business scenario, avoiding requesting too many permissions at once. The length of a permission name cannot exceed 256 characters. Valid permission names can be queried in the [Application Permission List](../../security/AccessToken/cj-app-permissions.md). |
| requestCallback | AsyncCallback\<[PermissionRequestResult](cj-apis-sercurity-permission_request_result.md#class-permissionrequestresultarraystring-arrayint32-arraybool)> | Yes | - | Callback function. After the call is complete, error information is returned through **err**, and the permission request result object is returned through **data**. The developer can determine whether the user has authorized based on the permission request result. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Access Control Error Codes](./cj-errorcode-access-token.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 12100001 | Invalid parameter. The context is invalid when it does not belong to the application itself. |

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The context is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.*

try {
    // The following code can be added to the dependency definitions
    var resultCallback = {
        errorCode: Option<BusinessException>, data: Option<PermissionRequestResult> => match (errorCode) {
            case Some(e) => Hilog.error(0, "AppLogCj", "permissionResultCallBack request error: errcode is ${e.code}")
            case _ =>
                match (data) {
                    case Some(value) =>
                        for (i in (0..value.permissions.size)) {
                            Hilog.info(0, "AppLogCj", "CallBack: ${value.permissions[i]} - ${value.authResults[i]}")
                        }
                    case _ => Hilog.error(0, "AppLogCj", "permissionResultCallBack request error: data is null")
                }
        }
    }

    let ctx = Global.abilityContext // Context application context needs to be obtained. For details, see the Usage Instructions in this document.
    let atManager = AbilityAccessCtrl.createAtManager()
    let permissionList = ["ohos.permission.READ_CONTACTS", "ohos.permission.CAMERA"]
    atManager.requestPermissionsFromUser(ctx.getOrThrow(), permissionList, resultCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## enum GrantStatus

```cangjie
public enum GrantStatus <: Equatable<GrantStatus> & ToString {
    | PermissionDenied
    | PermissionGranted
    | ...
}
```

**Description:** Represents the authorization status.

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 22

**Parent Types:**

- Equatable\<GrantStatus>
- ToString

### PermissionDenied

```cangjie
PermissionDenied
```

**Description:** Not authorized.

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 22

### PermissionGranted

```cangjie
PermissionGranted
```

**Description:** Authorized.

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 22

### func !=(GrantStatus)

```cangjie
public operator func !=(other: GrantStatus): Bool
```

**Description:** Checks for inequality of authorization statuses.

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [GrantStatus](#enum-grantstatus) | Yes | - | Authorization status. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns true if the authorization statuses are different, otherwise returns false. |

### func ==(GrantStatus)

```cangjie
public operator func ==(other: GrantStatus): Bool
```

**Description:** Checks for equality of authorization statuses.

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [GrantStatus](#enum-grantstatus) | Yes | - | Authorization status. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns true if the authorization statuses are the same, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Returns the string representation of the authorization status.

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| String | String representation of the authorization status. |

## type Permissions

```cangjie
public type Permissions = String
```

**Description:** [Permissions](#type-permissions) is an alias for the String type.