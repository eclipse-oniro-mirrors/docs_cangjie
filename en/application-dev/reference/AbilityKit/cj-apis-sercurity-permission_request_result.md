# ohos.security.permission_request_result (PermissionRequestResult)

The PermissionRequestResult object is returned when calling [requestPermissionsFromUser](cj-apis-ability_access_ctrl.md#func-requestpermissionsfromuseruiabilitycontext-arraypermissions-asynccallbackpermissionrequestresult) to request permissions, indicating the result of the permission request.

## Import Module

```cangjie
import kit.AbilityKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample project and configuration template, please refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

### class PermissionRequestResult(Array\<String>, Array\<Int32>, ?Array\<Bool>)

```cangjie
public class PermissionRequestResult {
    public var permissions: Array<String>
    public var authResults: Array<Int32>
    public var dialogShownResults = Array<Bool>()
}
```

**Function:** Constructs a permission request result object.

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 21

### var authResults

```cangjie
public var authResults: Array<Int32>
```

**Function:** The results of the corresponding requested permissions. -1: Not granted. 0: Granted. 2: Not granted, indicating the request is invalid. Possible reasons include: the target permission is not declared in the configuration file; the permission name is invalid; some permissions have special application conditions that were not met when requesting the corresponding permission.

**Type:** Array<\Int32>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 21

### var dialogShownResults

```cangjie
public var dialogShownResults = Array<Bool>()
```

**Function:** Indicates whether a dialog was shown for this permission request: true: Dialog shown. false: No dialog shown.

**Type:** Array<\Bool>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 21

### var permissions

```cangjie
public var permissions: Array<String>
```

**Function:** The permissions passed by the user.

**Type:** Array<\String>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Security.AccessToken

**Since:** 21