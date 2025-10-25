# ohos.security.huks

Provides applications with keystore capabilities, including key management and cryptographic operations.

Keys managed by HUKS can be either imported by applications or generated through HUKS interfaces.

## Import Module

```cangjie
import kit.UniversalKeystoreKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## func abortSession(HuksHandleId, HuksOptions)

```cangjie

public func abortSession(handle: HuksHandleId, options: HuksOptions): Unit
```

**Description:** Interface for aborting a key operation session.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| handle | [HuksHandleId](#class-hukshandleid) | Yes | - | The handle for the abortSession operation. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | The parameter set for the abortSession operation. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Argument is invalid |
  | 801 | API is not supported |
  | 12000004 | Operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | Error occurred in crypto engine |
  | 12000012 | External error |
  | 12000014 | Memory is insufficient |

## func anonAttestKeyItem(String, HuksOptions)

```cangjie

public func anonAttestKeyItem(keyAlias: String, options: HuksOptions): Array<String>
```

**Description:** Obtains an anonymous key certificate. This operation requires network connectivity and may take a long time.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | The key alias, which stores the alias of the key for which the certificate is to be obtained. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Specifies the required parameters and data when obtaining the certificate. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | Returns the key certificate chain. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Check permission failed |
  | 401 | Argument is invalid |
  | 801 | API is not supported |
  | 12000001 | Algorithm mode is not supported |
  | 12000002 | Algorithm parameter is missing |
  | 12000003 | Algorithm parameter is invalid |
  | 12000004 | Operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | Error occurred in crypto engine |
  | 12000011 | Queried entity does not exist |
  | 12000012 | External error |
  | 12000014 | Memory is insufficient |

## func deleteKeyItem(String, HuksOptions)

```cangjie

public func deleteKeyItem(keyAlias: String, options: HuksOptions): Unit
```

**Description:** Deletes a key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | The key alias, which should be the same as the alias used when generating the key. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Specifies the key attribute Tag for deletion, such as the scope of deletion (all/single). When deleting a single key, the Tag field can be left empty. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Argument is invalid |
  | 801 | API is not supported |
  | 12000004 | Operating file failed |
  | 12000005 | IPC communication failed |
  | 12000011 | Queried entity does not exist |
  | 12000012 | External error |
  | 12000014 | Memory is insufficient |

## func exportKeyItem(String, HuksOptions)

```cangjie

public func exportKeyItem(keyAlias: String, _: HuksOptions): Bytes
```

**Description:** Exports a key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | The key alias, which should be the same as the alias used when generating the key. |
| _ | [HuksOptions](#class-huksoptions) | Yes | - | An empty object (pass empty here). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bytes | Returns the public key exported from the key. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Argument is invalid |
  | 801 | API is not supported |
  | 12000001 | Algorithm mode is not supported |
  | 12000002 | Algorithm parameter is missing |
  | 12000003 | Algorithm parameter is invalid |
  | 12000004 | Operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | Error occurred in crypto engine |
  | 12000011 | Queried entity does not exist |
  | 12000012 | External error |
  | 12000014 | Memory is insufficient |

## func finishSession(HuksHandleId, HuksOptions, Bytes)

```cangjie

public func finishSession(handle: HuksHandleId, options: HuksOptions, token!: Bytes): Option<Bytes>
```

**Description:** Interface for finishing a key operation session. [security_huks.initSession](#func-initsessionstring-huksoptions), [security_huks.updateSession](#func-updatesessionhukshandleid-huksoptions-bytes), and [security_huks.finishSession](#func-finishsessionhukshandleid-huksoptions-bytes) are three-stage interfaces that must be used together.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| handle | [HuksHandleId](#class-hukshandleid) | Yes | - | The handle for the finishSession operation. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | The parameter set for the finishSession operation. |
| token | Bytes | No | Bytes\<UInt8>() | Represents the value of the AuthToken from the USER IAM service. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<Bytes> | Represents the value of the AuthToken from the USER IAM service. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3. Parameter verification failed. |
  | 801 | API is not supported |
  | 12000001 | Algorithm mode is not supported |
  | 12000002 | Algorithm parameter is missing |
  | 12000003 | Algorithm parameter is invalid |
  | 12000004 | Operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | Error occurred in crypto engine |
  | 12000007 | This credential is already invalidated permanently |
  | 12000008 | Verify auth token failed |
  | 12000009 | Auth token is already timeout |
  | 12000011 | Queried entity does not exist |
  | 12000012 | Device environment or input parameter abnormal |
  | 12000014 | Memory is insufficient |

## func generateKeyItem(String, HuksOptions)

```cangjie

public func generateKeyItem(keyAlias: String, options: HuksOptions): Unit
```

**Description:** Generates a key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | The key alias. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Stores the required Tags for key generation. The algorithm, key purpose, and key length are mandatory parameters. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Argument is invalid |
  | 801 | API is not supported |
  | 12000001 | Algorithm mode is not supported |
  | 12000002 | Algorithm parameter is missing |
  | 12000003 | Algorithm parameter is invalid |
  | 12000004 | Operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | Error occurred in crypto engine |
  | 12000012 | External error |
  | 12000013 | Queried credential does not exist |
  | 12000014 | Memory is insufficient |
  | 12000015 | Call service failed |

## func getKeyItemProperties(String, HuksOptions)

```cangjie

public func getKeyItemProperties(keyAlias: String, _: HuksOptions): Array<HuksParam>
```

**Description:** Retrieves key properties.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | The key alias. |
| _ | [HuksOptions](#class-huksoptions) | Yes | - | An empty object (pass empty here). |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[HuksParam](#class-huksparam)> | Returns the key properties. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Argument is invalid |
  | 801 | API is not supported |
  | 12000001 | Algorithm mode is not supported |
  | 12000002 | Algorithm parameter is missing |
  | 12000003 | Algorithm parameter is invalid |
  | 12000004 | Operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | Error occurred in crypto engine |
  | 12000011 | Queried entity does not exist |
  | 12000012 | External error |
  | 12000014 | Memory is insufficient |

## func importKeyItem(String, HuksOptions)

```cangjie

public func importKeyItem(keyAlias: String, options: HuksOptions): Unit
```

**Description:** Imports a plaintext key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | The key alias. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Specifies the required Tags and the key to be imported during import. The algorithm, key purpose, and key length are mandatory parameters. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Argument is invalid |
  | 801 | API is not supported |
  | 12000001 | Algorithm mode is not supported |
  | 12000002 | Algorithm parameter is missing |
  | 12000003 | Algorithm parameter is invalid |
  | 12000004 | Operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | Error occurred in crypto engine |
  | 12000011 | Queried entity does not exist |
  | 12000012 | External error |
  | 12000013 | Queried credential does not exist |
  | 12000014 | Memory is insufficient |
  | 12000015 | Call service failed |

## func importWrappedKeyItem(String, String, HuksOptions)

```cangjie

public func importWrappedKeyItem(keyAlias: String, wrappingKeyAlias: String, options: HuksOptions): Unit
```

**Description:** Imports an encrypted key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | The key alias, which stores the alias of the key to be imported. |
| wrappingKeyAlias | String | Yes | - | The key alias, corresponding to the key used to decrypt the encrypted key data. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Specifies the required Tags and the encrypted key data to be imported during import. The algorithm, key purpose, and key length are mandatory parameters. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Argument is invalid |
  | 801 | API is not supported |
  | 12000001 | Algorithm mode is not supported |
  | 12000002 | Algorithm parameter is missing |
  | 12000003 | Algorithm parameter is invalid |
  | 12000004 | Operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | Error occurred in crypto engine |
  | 12000011 | Queried entity does not exist |
  | 12000012 | External error |
  | 12000013 | Queried credential does not exist |
  | 12000014 | Memory is insufficient |
  | 12000015 | Call service failed |

## func initSession(String, HuksOptions)

```cangjie

public func initSession(keyAlias: String, options: HuksOptions): HuksSessionHandle
```

**Description:** Interface for initializing a key operation session. [security_huks.initSession](#func-initsessionstring-huksoptions), [security_huks.updateSession](#func-updatesessionhukshandleid-huksoptions-bytes), and [security_huks.finishSession](#func-finishsessionhukshandleid-huksoptions-bytes) are three-stage interfaces that must be used together.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | The key alias for the initSession operation. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | The parameter set for the initSession operation. |

**Return Value:**

| Type | Description |
|:----|:----|
| [HuksSessionHandle](#class-hukssessionhandle) | Returns the HUKS handle for the key. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode## func isKeyItemExist(String, HuksOptions)

```cangjie
public func isKeyItemExist(keyAlias: String, options: HuksOptions): Bool
```

**Function:** Checks whether a key exists.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | Alias of the key to be queried. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Specifies the attribute Tag for key query, such as query scope (all/single). When querying a single key, the Tag field can be left empty. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Indicates whether the key exists. |

**Exceptions:**

- BusinessException: Error codes are listed in the following table. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | argument is invalid |
  | 801 | api is not supported |
  | 12000002 | algorithm param is missing |
  | 12000003 | algorithm param is invalid |
  | 12000004 | operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | error occurred in crypto engine |
  | 12000012 | external error |
  | 12000014 | memory is insufficient |

## func updateSession(HuksHandleId, HuksOptions, Bytes)

```cangjie
public func updateSession(handle: HuksHandleId, options: HuksOptions, token!: Bytes): Option<Bytes>
```

**Function:** Updates the session for key operations. [security_huks.initSession](#func-initsessionstring-huksoptions), [security_huks.updateSession](#func-updatesessionhukshandleid-huksoptions-bytes), and [security_huks.finishSession](#func-finishsessionhukshandleid-huksoptions-bytes) are three-phase APIs that must be used together.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| handle | [HuksHandleId](#class-hukshandleid) | Yes | - | Handle for the updateSession operation. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Parameter set for updateSession. |
| token | Bytes | No | Bytes\<UInt8>() | Represents the AuthToken value from the USER IAM service. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<Bytes> | Outputs the key update result. |

**Exceptions:**

- BusinessException: Error codes are listed in the following table. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. 3. Parameter verification failed. |
  | 801 | api is not supported |
  | 12000001 | algorithm mode is not supported |
  | 12000002 | algorithm param is missing |
  | 12000003 | algorithm param is invalid |
  | 12000004 | operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | error occurred in crypto engine |
  | 12000007 | this credential is already invalidated permanently |
  | 12000008 | verify auth token failed |
  | 12000009 | auth token is already timeout |
  | 12000011 | queried entity does not exist |
  | 12000012 | Device environment or input parameter abnormal |
  | 12000014 | memory is insufficient |

## class HuksAuthAccessType

```cangjie
public class HuksAuthAccessType {
    public static const HUKS_AUTH_ACCESS_INVALID_CLEAR_PASSWORD: UInt32 = 1 << 0
    public static const HUKS_AUTH_ACCESS_INVALID_NEW_BIO_ENROLL: UInt32 = 1 << 1
}
```

**Function:** Represents security access control types.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_AUTH_ACCESS_INVALID_CLEAR_PASSWORD

```cangjie
public static const HUKS_AUTH_ACCESS_INVALID_CLEAR_PASSWORD: UInt32 = 1 << 0
```

**Function:** Indicates that the key is always valid.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_AUTH_ACCESS_INVALID_NEW_BIO_ENROLL

```cangjie
public static const HUKS_AUTH_ACCESS_INVALID_NEW_BIO_ENROLL: UInt32 = 1 << 1
```

**Function:** Indicates that the key becomes invalid after the password is cleared.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

## class HuksAuthStorageLevel

```cangjie
public class HuksAuthStorageLevel {
    public static const HUKS_AUTH_STORAGE_LEVEL_DE: UInt32 = 0
    public static const HUKS_AUTH_STORAGE_LEVEL_CE: UInt32 = 1
    public static const HUKS_AUTH_STORAGE_LEVEL_ECE: UInt32 = 2
}
```

**Function:** Specifies the storage security level for keys during generation or import.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_AUTH_STORAGE_LEVEL_CE

```cangjie
public static const HUKS_AUTH_STORAGE_LEVEL_CE: UInt32 = 1
```

**Function:** Indicates that the key is accessible only after the first unlock.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_AUTH_STORAGE_LEVEL_DE

```cangjie
public static const HUKS_AUTH_STORAGE_LEVEL_DE: UInt32 = 0
```

**Function:** Indicates that the key is accessible only after booting.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_AUTH_STORAGE_LEVEL_ECE

```cangjie
public static const HUKS_AUTH_STORAGE_LEVEL_ECE: UInt32 = 2
```

**Function:** Indicates that the key is accessible only in the unlocked state.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksChallengePosition

```cangjie
public class HuksChallengePosition {
    public static const HUKS_CHALLENGE_POS_0: UInt32 = 0
    public static const HUKS_CHALLENGE_POS_1: UInt32 = 1
    public static const HUKS_CHALLENGE_POS_2: UInt32 = 2
    public static const HUKS_CHALLENGE_POS_3: UInt32 = 3
}
```

**Function:** When the challenge type is user-defined, the generated challenge has an effective length of only 8 consecutive bytes and supports only 4 positions.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_CHALLENGE_POS_0

```cangjie
public static const HUKS_CHALLENGE_POS_0: UInt32 = 0
```

**Function:** Indicates that bytes 0~7 are the valid challenge for the current key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_CHALLENGE_POS_1

```cangjie
public static const HUKS_CHALLENGE_POS_1: UInt32 = 1
```

**Function:** Indicates that bytes 8~15 are the valid challenge for the current key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_CHALLENGE_POS_2

```cangjie
public static const HUKS_CHALLENGE_POS_2: UInt32 = 2
```

**Function:** Indicates that bytes 16~23 are the valid challenge for the current key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_CHALLENGE_POS_3

```cangjie
public static const HUKS_CHALLENGE_POS_3: UInt32 = 3
```

**Function:** Indicates that bytes 24~31 are the valid challenge for the current key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

## class HuksChallengeType

```cangjie
public class HuksChallengeType {
    public static const HUKS_CHALLENGE_TYPE_NORMAL: UInt32 = 0
    public static const HUKS_CHALLENGE_TYPE_CUSTOM: UInt32 = 1
    public static const HUKS_CHALLENGE_TYPE_NONE: UInt32 = 2
}
```

**Function:** Represents the type of challenge generated during key usage.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_CHALLENGE_TYPE_CUSTOM

```cangjie
public static const HUKS_CHALLENGE_TYPE_CUSTOM: UInt32 = 1
```

**Function:** Indicates a user-defined challenge type. Supports one-time authentication for multiple keys.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_CHALLENGE_TYPE_NONE

```cangjie
public static const HUKS_CHALLENGE_TYPE_NONE: UInt32 = 2
```

**Function:** Indicates a no-challenge type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_CHALLENGE_TYPE_NORMAL

```cangjie
public static const HUKS_CHALLENGE_TYPE_NORMAL: UInt32 = 0
```

**Function:** Indicates a normal challenge type, with a default length of 32 bytes.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

## class HuksCipherMode

```cangjie
public class HuksCipherMode {
    public static const HUKS_MODE_ECB: UInt32 = 1
    public static const HUKS_MODE_CBC: UInt32 = 2
    public static const HUKS_MODE_CTR: UInt32 = 3
    public static const HUKS_MODE_OFB: UInt32 = 4
    public static const HUKS_MODE_CCM: UInt32 = 31
    public static const HUKS_MODE_GCM: UInt32 = 32
}
```

**Function:** Represents encryption modes.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_MODE_CBC

```cangjie
public static const HUKS_MODE_CBC: UInt32 = 2
```

**Function:** Indicates CBC encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_MODE_CCM

```cangjie
public static const HUKS_MODE_CCM: UInt32 = 31
```

**Function:** Indicates CCM encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_MODE_CTR

```cangjie
public static const HUKS_MODE_CTR: UInt32 = 3
```

**Function:** Indicates CTR encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_MODE_ECB

```cangjie
public static const HUKS_MODE_ECB: UInt32 = 1
```

**Function:** Indicates ECB encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_MODE_GCM

```cangjie
public static const HUKS_MODE_GCM: UInt32 = 32
```

**Function:** Indicates GCM encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_MODE_OFB

```cangjie
public static const HUKS_MODE_OFB: UInt32 = 4
```

**Function:** Indicates OFB encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21## class HuksHandleId

```cangjie
public class HuksHandleId {}
```

**Description:** The ID of an encryption handle.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

## class HuksImportKeyType

```cangjie
public class HuksImportKeyType {
    public static const HUKS_KEY_TYPE_PUBLIC_KEY: UInt32 = 0
    public static const HUKS_KEY_TYPE_PRIVATE_KEY: UInt32 = 1
    public static const HUKS_KEY_TYPE_KEY_PAIR: UInt32 = 2
}
```

**Description:** Indicates the type of key to be imported. The default is public key. This field is not required when importing symmetric keys.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_TYPE_KEY_PAIR

```cangjie
public static const HUKS_KEY_TYPE_KEY_PAIR: UInt32 = 2
```

**Description:** Indicates the key type to be imported is a public-private key pair.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_TYPE_PRIVATE_KEY

```cangjie
public static const HUKS_KEY_TYPE_PRIVATE_KEY: UInt32 = 1
```

**Description:** Indicates the key type to be imported is a private key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_TYPE_PUBLIC_KEY

```cangjie
public static const HUKS_KEY_TYPE_PUBLIC_KEY: UInt32 = 0
```

**Description:** Indicates the key type to be imported is a public key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksKeyAlg

```cangjie
public class HuksKeyAlg {
    public static const HUKS_ALG_RSA: UInt32 = 1
    public static const HUKS_ALG_ECC: UInt32 = 2
    public static const HUKS_ALG_DSA: UInt32 = 3
    public static const HUKS_ALG_AES: UInt32 = 20
    public static const HUKS_ALG_HMAC: UInt32 = 50
    public static const HUKS_ALG_HKDF: UInt32 = 51
    public static const HUKS_ALG_PBKDF2: UInt32 = 52
    public static const HUKS_ALG_ECDH: UInt32 = 100
    public static const HUKS_ALG_X25519: UInt32 = 101
    public static const HUKS_ALG_ED25519: UInt32 = 102
    public static const HUKS_ALG_DH: UInt32 = 103
    public static const HUKS_ALG_SM2: UInt32 = 150
    public static const HUKS_ALG_SM3: UInt32 = 151
    public static const HUKS_ALG_SM4: UInt32 = 152
}
```

**Description:** Indicates the algorithm used by the key.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_AES

```cangjie
public static const HUKS_ALG_AES: UInt32 = 20
```

**Description:** Indicates the use of AES algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_DH

```cangjie
public static const HUKS_ALG_DH: UInt32 = 103
```

**Description:** Indicates the use of DH algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_DSA

```cangjie
public static const HUKS_ALG_DSA: UInt32 = 3
```

**Description:** Indicates the use of DSA algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_ECC

```cangjie
public static const HUKS_ALG_ECC: UInt32 = 2
```

**Description:** Indicates the use of ECC algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_ECDH

```cangjie
public static const HUKS_ALG_ECDH: UInt32 = 100
```

**Description:** Indicates the use of ECDH algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_ED25519

```cangjie
public static const HUKS_ALG_ED25519: UInt32 = 102
```

**Description:** Indicates the use of ED25519 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_HKDF

```cangjie
public static const HUKS_ALG_HKDF: UInt32 = 51
```

**Description:** Indicates the use of HKDF algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_HMAC

```cangjie
public static const HUKS_ALG_HMAC: UInt32 = 50
```

**Description:** Indicates the use of HMAC algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_PBKDF2

```cangjie
public static const HUKS_ALG_PBKDF2: UInt32 = 52
```

**Description:** Indicates the use of PBKDF2 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_RSA

```cangjie
public static const HUKS_ALG_RSA: UInt32 = 1
```

**Description:** Indicates the use of RSA algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_SM2

```cangjie
public static const HUKS_ALG_SM2: UInt32 = 150
```

**Description:** Indicates the use of SM2 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_SM3

```cangjie
public static const HUKS_ALG_SM3: UInt32 = 151
```

**Description:** Indicates the use of SM3 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_SM4

```cangjie
public static const HUKS_ALG_SM4: UInt32 = 152
```

**Description:** Indicates the use of SM4 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ALG_X25519

```cangjie
public static const HUKS_ALG_X25519: UInt32 = 101
```

**Description:** Indicates the use of X25519 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksKeyDigest

```cangjie
public class HuksKeyDigest {
    public static const HUKS_DIGEST_NONE: UInt32 = 0
    public static const HUKS_DIGEST_MD5: UInt32 = 1
    public static const HUKS_DIGEST_SM3: UInt32 = 2
    public static const HUKS_DIGEST_SHA1: UInt32 = 10
    public static const HUKS_DIGEST_SHA224: UInt32 = 11
    public static const HUKS_DIGEST_SHA256: UInt32 = 12
    public static const HUKS_DIGEST_SHA384: UInt32 = 13
    public static const HUKS_DIGEST_SHA512: UInt32 = 14
}
```

**Description:** Indicates the digest algorithm.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_DIGEST_MD5

```cangjie
public static const HUKS_DIGEST_MD5: UInt32 = 1
```

**Description:** Indicates the MD5 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_DIGEST_NONE

```cangjie
public static const HUKS_DIGEST_NONE: UInt32 = 0
```

**Description:** Indicates no digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_DIGEST_SHA1

```cangjie
public static const HUKS_DIGEST_SHA1: UInt32 = 10
```

**Description:** Indicates the SHA1 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_DIGEST_SHA224

```cangjie
public static const HUKS_DIGEST_SHA224: UInt32 = 11
```

**Description:** Indicates the SHA224 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_DIGEST_SHA256

```cangjie
public static const HUKS_DIGEST_SHA256: UInt32 = 12
```

**Description:** Indicates the SHA256 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_DIGEST_SHA384

```cangjie
public static const HUKS_DIGEST_SHA384: UInt32 = 13
```

**Description:** Indicates the SHA384 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_DIGEST_SHA512

```cangjie
public static const HUKS_DIGEST_SHA512: UInt32 = 14
```

**Description:** Indicates the SHA512 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_DIGEST_SM3

```cangjie
public static const HUKS_DIGEST_SM3: UInt32 = 2
```

**Description:** Indicates the SM3 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksKeyFlag

```cangjie
public class HuksKeyFlag {
    public static const HUKS_KEY_FLAG_IMPORT_KEY: UInt32 = 1
    public static const HUKS_KEY_FLAG_GENERATE_KEY: UInt32 = 2
    public static const HUKS_KEY_FLAG_AGREE_KEY: UInt32 = 3
    public static const HUKS_KEY_FLAG_DERIVE_KEY: UInt32 = 4
}
```

**Description:** Indicates the key generation method.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_FLAG_AGREE_KEY

```cangjie
public static const HUKS_KEY_FLAG_AGREE_KEY: UInt32 = 3
```

**Description:** Indicates a key generated through key agreement interface.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_FLAG_DERIVE_KEY

```cangjie
public static const HUKS_KEY_FLAG_DERIVE_KEY: UInt32 = 4
```

**Description:** Indicates a key generated through key derivation interface.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_FLAG_GENERATE_KEY

```cangjie
public static const HUKS_KEY_FLAG_GENERATE_KEY: UInt32 = 2
```

**Description:** Indicates a key generated through key generation interface.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_FLAG_IMPORT_KEY

```cangjie
public static const HUKS_KEY_FLAG_IMPORT_KEY: UInt32 = 1
```

**Description:** Indicates a key imported through public key import interface.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksKeyGenerateType

```cangjie
public class HuksKeyGenerateType {
    public static const HUKS_KEY_GENERATE_TYPE_DEFAULT: UInt32 = 0
    public static const HUKS_KEY_GENERATE_TYPE_DERIVE: UInt32 = 1
    public static const HUKS_KEY_GENERATE_TYPE_AGREE: UInt32 = 2
}
```

**Description:** Indicates the type of key generation.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_GENERATE_TYPE_AGREE

```cangjie
public static const HUKS_KEY_GENERATE_TYPE_AGREE: UInt32 = 2
```

**Description:** Key generated through agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_GENERATE_TYPE_DEFAULT

```cangjie
public static const HUKS_KEY_GENERATE_TYPE_DEFAULT: UInt32 = 0
```

**Description:** Default generated key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_GENERATE_TYPE_DERIVE

```cangjie
public static const HUKS_KEY_GENERATE_TYPE_DERIVE: UInt32 = 1
```

**Description:** Key generated through derivation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksKeyPadding

```cangjie
public class HuksKeyPadding {
    public static const HUKS_PADDING_NONE: UInt32 = 0
    public static const HUKS_PADDING_OAEP: UInt32 = 1
    public static const HUKS_PADDING_PSS: UInt32 = 2
    public static const HUKS_PADDING_PKCS1_V1_5: UInt32 = 3
    public static const HUKS_PADDING_PKCS5: UInt32 = 4
    public static const HUKS_PADDING_PKCS7: UInt32 = 5
}
```

**Description:** Indicates padding algorithms.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_PADDING_NONE

```cangjie
public static const HUKS_PADDING_NONE: UInt32 = 0
```

**Description:** Indicates no padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_PADDING_OAEP

```cangjie
public static const HUKS_PADDING_OAEP: UInt32 = 1
```

**Description:** Indicates OAEP padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_PADDING_PKCS1_V1_5

```cangjie
public static const HUKS_PADDING_PKCS1_V1_5: UInt32 = 3
```

**Description:** Indicates PKCS1_V1_5 padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_PADDING_PKCS5

```cangjie
public static const HUKS_PADDING_PKCS5: UInt32 = 4
```

**Description:** Indicates PKCS5 padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_PADDING_PKCS7

```cangjie
public static const HUKS_PADDING_PKCS7: UInt32 = 5
```

**Description:** Indicates PKCS7 padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_PADDING_PSS

```cangjie
public static const HUKS_PADDING_PSS: UInt32 = 2
```

**Description:** Indicates PSS padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksKeyPurpose

```cangjie
public class HuksKeyPurpose {
    public static const HUKS_KEY_PURPOSE_ENCRYPT: UInt32 = 1
    public static const HUKS_KEY_PURPOSE_DECRYPT: UInt32 = 2
    public static const HUKS_KEY_PURPOSE_SIGN: UInt32 = 4
    public static const HUKS_KEY_PURPOSE_VERIFY: UInt32 = 8
    public static const HUKS_KEY_PURPOSE_DERIVE: UInt32 = 16
    public static const HUKS_KEY_PURPOSE_WRAP: UInt32 = 32
    public static const HUKS_KEY_PURPOSE_UNWRAP: UInt32 = 64
    public static const HUKS_KEY_PURPOSE_MAC: UInt32 = 128
    public static const HUKS_KEY_PURPOSE_AGREE: UInt32 = 256
}
```

**Description:** Indicates key purposes.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_PURPOSE_AGREE

```cangjie
public static const HUKS_KEY_PURPOSE_AGREE: UInt32 = 256
```

**Description:** Indicates the key is used for key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_PURPOSE_DECRYPT

```cangjie
public static const HUKS_KEY_PURPOSE_DECRYPT: UInt32 = 2
```

**Description:** Indicates the key is used for decrypting ciphertext.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_PURPOSE_DERIVE

```cangjie
public static const HUKS_KEY_PURPOSE_DERIVE: UInt32 = 16
```

**Description:** Indicates the key is used for key derivation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_PURPOSE_ENCRYPT

```cangjie
public static const HUKS_KEY_PURPOSE_ENCRYPT: UInt32 = 1
```

**Description:** Indicates the key is used for encrypting plaintext.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_PURPOSE_MAC

```cangjie
public static const HUKS_KEY_PURPOSE_MAC: UInt32 = 128
```

**Description:** Indicates the key is used for generating MAC (Message Authentication Code).

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_PURPOSE_SIGN

```cangjie
public static const HUKS_KEY_PURPOSE_SIGN: UInt32 = 4
```

**Description:** Indicates the key is used for encrypted import.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_PURPOSE_UNWRAP

```cangjie
public static const HUKS_KEY_PURPOSE_UNWRAP: UInt32 = 64
```

**Description:** Indicates the key is used for encrypted import.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_PURPOSE_VERIFY

```cangjie
public static const HUKS_KEY_PURPOSE_VERIFY: UInt32 = 8
```

**Description:** Indicates the key is used for verifying signed data.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_KEY_PURPOSE_WRAP

```cangjie
public static const HUKS_KEY_PURPOSE_WRAP: UInt32 = 32
```

**Description:** Indicates the key is used for encrypted export.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksKeySize

```cangjie
public class HuksKeySize {
    public static const HUKS_RSA_KEY_SIZE_512: UInt32 = 512
    public static const HUKS_RSA_KEY_SIZE_768: UInt32 = 768
    public static const HUKS_RSA_KEY_SIZE_1024: UInt32 = 1024
    public static const HUKS_RSA_KEY_SIZE_2048: UInt32 = 2048
    public static const HUKS_RSA_KEY_SIZE_3072: UInt32 = 3072
    public static const HUKS_RSA_KEY_SIZE_4096: UInt32 = 4096
    public static const HUKS_ECC_KEY_SIZE_224: UInt32 = 224
    public static const HUKS_ECC_KEY_SIZE_256: UInt32 = 256
    public static const HUKS_ECC_KEY_SIZE_384: UInt32 = 384
    public static const HUKS_ECC_KEY_SIZE_521: UInt32 = 521
    public static const HUKS_AES_KEY_SIZE_128: UInt32 = 128
    public static const HUKS_AES_KEY_SIZE_192: UInt32 = 192
    public static const HUKS_AES_KEY_SIZE_256: UInt32 = 256
    public static const HUKS_CURVE25519_KEY_SIZE_256: UInt32 = 256
    public static const HUKS_DH_KEY_SIZE_2048: UInt32 = 2048
    public static const HUKS_DH_KEY_SIZE_3072: UInt32 = 3072
    public static const HUKS_DH_KEY_SIZE_4096: UInt32 = 4096
    public static const HUKS_SM2_KEY_SIZE_256: UInt32 = 256
    public static const HUKS_SM4_KEY_SIZE_128: UInt32 = 128
}
```

**Description:** Indicates key lengths.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_AES_KEY_SIZE_128

```cangjie
public static const HUKS_AES_KEY_SIZE_128: UInt32 = 128
```

**Description:** Indicates the key length of 3DES algorithm is 128 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_AES_KEY_SIZE_192

```cangjie
public static const HUKS_AES_KEY_SIZE_192: UInt32 = 192
```

**Description:** Indicates the key length of 3DES algorithm is 192 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_AES_KEY_SIZE_256

```cangjie
public static const HUKS_AES_KEY_SIZE_256: UInt32 = 256
```

**Description:** Indicates the key length of AES algorithm is 256 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_CURVE25519_KEY_SIZE_256

```cangjie
public static const HUKS_CURVE25519_KEY_SIZE_256: UInt32 = 256
```

**Description:** Indicates the key length of CURVE25519 algorithm is 256 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_DH_KEY_SIZE_2048

```cangjie
public static const HUKS_DH_KEY_SIZE_2048: UInt32 = 2048
```

**Description:** Indicates the key length of DH algorithm is 2048 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_DH_KEY_SIZE_3072

```cangjie
public static const HUKS_DH_KEY_SIZE_3072: UInt32 = 3072
```

**Description:** Indicates the key length of DH algorithm is 3072 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_DH_KEY_SIZE_4096

```cangjie
public static const HUKS_DH_KEY_SIZE_4096: UInt32 = 4096
```

**Description:** Indicates the key length of DH algorithm is 4096 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ECC_KEY_SIZE_224

```cangjie
public static const HUKS_ECC_KEY_SIZE_224: UInt32 = 224
```

**Description:** Indicates the key length of ECC algorithm is 224 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ECC_KEY_SIZE_256

```cangjie
public static const HUKS_ECC_KEY_SIZE_256: UInt32 = 256
```

**Description:** Indicates the key length of ECC algorithm is 256 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ECC_KEY_SIZE_384

```cangjie
public static const HUKS_ECC_KEY_SIZE_384: UInt32 = 384
```

**Description:** Indicates the key length of ECC algorithm is 384 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_ECC_KEY_SIZE_521

```cangjie
public static const HUKS_ECC_KEY_SIZE_521: UInt32 = 521
```

**Description:** Indicates the key length of ECC algorithm is 521 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_RSA_KEY_SIZE_1024

```cangjie
public static const HUKS_RSA_KEY_SIZE_1024: UInt32 = 1024
```

**Description:** Indicates the key length of RSA algorithm is 1024 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_RSA_KEY_SIZE_2048

```cangjie
public static const HUKS_RSA_KEY_SIZE_2048: UInt32 = 2048
```

**Description:** Indicates the key length of RSA algorithm is 2048 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_RSA_KEY_SIZE_3072

```cangjie
public static const HUKS_RSA_KEY_SIZE_3072: UInt32 = 3072
```

**Description:** Indicates the key length of RSA algorithm is 3072 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_RSA_KEY_SIZE## class HuksKeyStorageType

```cangjie
public class HuksKeyStorageType {
    public static const HUKS_STORAGE_ONLY_USED_IN_HUKS: UInt32 = 2
    public static const HUKS_STORAGE_KEY_EXPORT_ALLOWED: UInt32 = 3
}
```

**Description:** Represents key storage methods.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_STORAGE_KEY_EXPORT_ALLOWED

```cangjie
public static const HUKS_STORAGE_KEY_EXPORT_ALLOWED: UInt32 = 3
```

**Description:** Indicates that the key derived from the master key can be directly exported to the service provider, and HUKS does not provide hosting services for it.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_STORAGE_ONLY_USED_IN_HUKS

```cangjie
public static const HUKS_STORAGE_ONLY_USED_IN_HUKS: UInt32 = 2
```

**Description:** Indicates that the key derived from the master key is stored in HUKS and hosted by HUKS.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksOptions

```cangjie
public class HuksOptions {
    public var properties: Array<HuksParam>
    public var inData: Bytes

    public init(properties!: Array<HuksParam> = Array<HuksParam>(), inData!: Bytes = Bytes())
}
```

**Description:** Options used for interface calls.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### var inData

```cangjie
public var inData: Bytes
```

**Description:** Input data.

**Type:** Bytes

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### var properties

```cangjie
public var properties: Array<HuksParam>
```

**Description:** Properties, an array for storing HuksParam.

**Type:** Array\<[HuksParam](#class-huksparam)>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### init(Array\<HuksParam>, Bytes)

```cangjie

public init(properties!: Array<HuksParam> = Array<HuksParam>(), inData!: Bytes = Bytes())
```

**Description:** Constructs an instance of options for interface calls.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| properties | Array\<[HuksParam](#class-huksparam)> | No | Array<HuksParam>() | Properties, an array for storing HuksParam. |
| inData | Bytes | No | Bytes\<UInt8>() | Input data. |

## class HuksParam

```cangjie
public class HuksParam {
    public var tag: UInt32
    public var value: HuksParamValue

    public init(tag: UInt32, value: HuksParamValue)
}
```

**Description:** An element in the properties array of [HuksOptions](#class-huksoptions).

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### var tag

```cangjie
public var tag: UInt32
```

**Description:** Tag.

**Type:** UInt32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### var value

```cangjie
public var value: HuksParamValue
```

**Description:** Value corresponding to the tag.

**Type:** UInt32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### init(UInt32, HuksParamValue)

```cangjie

public init(tag: UInt32, value: HuksParamValue)
```

**Description:** Constructs an instance of an element in the properties array of [HuksOptions](#class-huksoptions).

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| tag | UInt32 | Yes | - | Tag. |
| value | [HuksParamValue](#enum-huksparamvalue) | Yes | - | Value corresponding to the tag. |

## class HuksRsaPssSaltLenType

```cangjie
public class HuksRsaPssSaltLenType {
    public static const HUKS_RSA_PSS_SALT_LEN_DIGEST: UInt32 = 0
    public static const HUKS_RSA_PSS_SALT_LEN_MAX: UInt32 = 1
}
```

**Description:** Represents the salt_len type required when RSA performs signing or verification with PSS padding.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_RSA_PSS_SALT_LEN_DIGEST

```cangjie
public static const HUKS_RSA_PSS_SALT_LEN_DIGEST: UInt32 = 0
```

**Description:** Indicates setting salt_len based on the digest length.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_RSA_PSS_SALT_LEN_MAX

```cangjie
public static const HUKS_RSA_PSS_SALT_LEN_MAX: UInt32 = 1
```

**Description:** Indicates setting salt_len based on the maximum length.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksSecureSignType

```cangjie
public class HuksSecureSignType {
    public static const HUKS_SECURE_SIGN_WITH_AUTHINFO: UInt32 = 1
}
```

**Description:** Represents the signature type specified when generating or importing a key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_SECURE_SIGN_WITH_AUTHINFO

```cangjie
public static const HUKS_SECURE_SIGN_WITH_AUTHINFO: UInt32 = 1
```

**Description:** Indicates the signature type carries authentication information. If this field is specified when generating or importing a key, authentication information will be added to the data to be signed before signing when using the key for signing.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

## class HuksSessionHandle

```cangjie
public class HuksSessionHandle {
    public var handle: HuksHandleId
    public var challenge: Bytes
}
```

**Description:** HUKS Handle structure.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### var challenge

```cangjie
public var challenge: Bytes
```

**Description:** Represents the challenge information obtained after the [initSession](#func-initsessionstring-huksoptions) operation.

**Type:** Bytes

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### var handle

```cangjie
public var handle: HuksHandleId
```

**Description:** Represents the handle value.

**Type:** [HuksHandleId](#class-hukshandleid)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksTagType

```cangjie
public class HuksTagType {
    public static const HUKS_TAG_TYPE_INVALID: UInt32 = 0 << 28
    public static const HUKS_TAG_TYPE_INT: UInt32 = 1 << 28
    public static const HUKS_TAG_TYPE_UINT: UInt32 = 2 << 28
    public static const HUKS_TAG_TYPE_ULONG: UInt32 = 3 << 28
    public static const HUKS_TAG_TYPE_BOOL: UInt32 = 4 << 28
    public static const HUKS_TAG_TYPE_BYTES: UInt32 = 5 << 28
}
```

**Description:** Represents the data type of a Tag.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_TYPE_BOOL

```cangjie
public static const HUKS_TAG_TYPE_BOOL: UInt32 = 4 << 28
```

**Description:** Indicates that the data type of the Tag is boolean.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_TYPE_BYTES

```cangjie
public static const HUKS_TAG_TYPE_BYTES: UInt32 = 5 << 28
```

**Description:** Indicates that the data type of the Tag is Uint8Array.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_TYPE_INT

```cangjie
public static const HUKS_TAG_TYPE_INT: UInt32 = 1 << 28
```

**Description:** Indicates that the data type of the Tag is UInt32.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_TYPE_INVALID

```cangjie
public static const HUKS_TAG_TYPE_INVALID: UInt32 = 0 << 28
```

**Description:** Indicates an invalid Tag type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_TYPE_UINT

```cangjie
public static const HUKS_TAG_TYPE_UINT: UInt32 = 2 << 28
```

**Description:** Indicates that the data type of the Tag is UInt32.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_TYPE_ULONG

```cangjie
public static const HUKS_TAG_TYPE_ULONG: UInt32 = 3 << 28
```

**Description:** Indicates that the data type of the Tag is bigint.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21## class HuksUnwrapSuite

```cangjie
public class HuksUnwrapSuite {
    public static const HUKS_UNWRAP_SUITE_X25519_AES_256_GCM_NOPADDING: UInt32 = 1
    public static const HUKS_UNWRAP_SUITE_ECDH_AES_256_GCM_NOPADDING: UInt32 = 2
}
```

**Description:** Represents algorithm suites for importing encrypted keys.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_UNWRAP_SUITE_ECDH_AES_256_GCM_NOPADDING

```cangjie
public static const HUKS_UNWRAP_SUITE_ECDH_AES_256_GCM_NOPADDING: UInt32 = 2
```

**Description:** Uses AES-256 GCM encryption after ECDH key agreement when importing encrypted keys.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_UNWRAP_SUITE_X25519_AES_256_GCM_NOPADDING

```cangjie
public static const HUKS_UNWRAP_SUITE_X25519_AES_256_GCM_NOPADDING: UInt32 = 1
```

**Description:** Uses AES-256 GCM encryption after X25519 key agreement when importing encrypted keys.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## class HuksUserAuthType

```cangjie
public class HuksUserAuthType {
    public static const HUKS_USER_AUTH_TYPE_FINGERPRINT: UInt32 = 1 << 0
    public static const HUKS_USER_AUTH_TYPE_FACE: UInt32 = 1 << 1
    public static const HUKS_USER_AUTH_TYPE_PIN: UInt32 = 1 << 2
}
```

**Description:** Represents user authentication types.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_USER_AUTH_TYPE_FACE

```cangjie
public static const HUKS_USER_AUTH_TYPE_FACE: UInt32 = 1 << 1
```

**Description:** Indicates facial recognition as the user authentication type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_USER_AUTH_TYPE_FINGERPRINT

```cangjie
public static const HUKS_USER_AUTH_TYPE_FINGERPRINT: UInt32 = 1 << 0
```

**Description:** Indicates fingerprint as the user authentication type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

### static const HUKS_USER_AUTH_TYPE_PIN

```cangjie
public static const HUKS_USER_AUTH_TYPE_PIN: UInt32 = 1 << 2
```

**Description:** Indicates PIN code as the user authentication type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 21

## enum CipherSpecItem

```cangjie
public enum CipherSpecItem <: Equatable<CipherSpecItem> & ToString {
    | OaepMdNameStr
    | OaepMgfNameStr
    | OaepMgf1MdStr
    | OaepMgf1PsrcUint8Arr
    | ...
}
```

**Description:** Enumerates cipher parameters that can be set via setCipherSpec interface or obtained via getCipherSpec interface.

**System Capability:** SystemCapability.Security.CryptoFramework.Cipher

**Since:** 21

**Parent Types:**

- Equatable\<CipherSpecItem>
- ToString

### func !=(CipherSpecItem)

```cangjie
public operator func !=(other: CipherSpecItem): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CipherSpecItem](#enum-cipherspecitem)|Yes|-|Another enum value.|

**Returns:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are unequal, otherwise false.|

### func ==(CipherSpecItem)

```cangjie
public operator func ==(other: CipherSpecItem): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CipherSpecItem](#enum-cipherspecitem)|Yes|-|Another enum value.|

**Returns:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enum values are equal, otherwise false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**System Capability:** SystemCapability.Security.CryptoFramework.Cipher

**Since:** 21

**Returns:**

|Type|Description|
|:----|:----|
|String|Description of the enum.|

## enum HuksParamValue

```cangjie
public enum HuksParamValue {
    | BooleanValue(Bool)
    | Int32Value(Int32)
    | Uint32Value(UInt32)
    | Uint64Value(UInt64)
    | BytesValue(Bytes)
    | ...
}
```

**Description:** Represents the value in HuksParam, supporting Bool, Int32, UInt32, UInt64, and Array\<UInt8> formats.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### BooleanValue(Bool)

```cangjie
BooleanValue(Bool)
```

**Description:** This field is used to pass Bool-type values.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### BytesValue(Bytes)

```cangjie
BytesValue(Bytes)
```

**Description:** This field is used to pass Bytes-type values.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### Int32Value(Int32)

```cangjie
Int32Value(Int32)
```

**Description:** This field is used to pass Int32-type values.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### Uint32Value(UInt32)

```cangjie
Uint32Value(UInt32)
```

**Description:** This field is used to pass UInt32-type values.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### Uint64Value(UInt64)

```cangjie
Uint64Value(UInt64)
```

**Description:** This field is used to pass UInt64-type values.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

## enum HuksTag

```cangjie
public class HuksTag {
    public static const HUKS_TAG_ALGORITHM: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 1
    public static const HUKS_TAG_PURPOSE: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 2
    public static const HUKS_TAG_KEY_SIZE: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 3
    public static const HUKS_TAG_DIGEST: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 4
    public static const HUKS_TAG_PADDING: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 5
    public static const HUKS_TAG_BLOCK_MODE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 6
    public static const HUKS_TAG_KEY_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 7
    public static const HUKS_TAG_ASSOCIATED_DATA: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 8
    public static const HUKS_TAG_NONCE: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 9
    public static const HUKS_TAG_IV: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 10
    public static const HUKS_TAG_INFO: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 11
    public static const HUKS_TAG_SALT: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 12
    public static const HUKS_TAG_ITERATION: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 14
    public static const HUKS_TAG_KEY_GENERATE_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 15
    public static const HUKS_TAG_AGREE_ALG: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 19
    public static const HUKS_TAG_AGREE_PUBLIC_KEY_IS_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 20
    public static const HUKS_TAG_AGREE_PRIVATE_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 21
    public static const HUKS_TAG_AGREE_PUBLIC_KEY: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 22
    public static const HUKS_TAG_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 23
    public static const HUKS_TAG_DERIVE_KEY_SIZE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 24
    public static const HUKS_TAG_IMPORT_KEY_TYPE: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 25
    public static const HUKS_TAG_UNWRAP_ALGORITHM_SUITE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 26
    public static const HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 29
    public static const HUKS_TAG_RSA_PSS_SALT_LEN_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 30
    public static const HUKS_TAG_USER_ID: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 302
    public static const HUKS_TAG_NO_AUTH_REQUIRED: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 303
    public static const HUKS_TAG_USER_AUTH_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 304
    public static const HUKS_TAG_AUTH_TIMEOUT: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 305
    public static const HUKS_TAG_AUTH_TOKEN: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 306
    public static const HUKS_TAG_KEY_AUTH_ACCESS_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 307
    public static const HUKS_TAG_KEY_SECURE_SIGN_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 308
    public static const HUKS_TAG_CHALLENGE_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 309
    public static const HUKS_TAG_CHALLENGE_POS: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 310
    public static const HUKS_TAG_KEY_AUTH_PURPOSE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 311
    public static const HUKS_TAG_AUTH_STORAGE_LEVEL: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 316
    public static const HUKS_TAG_ATTESTATION_CHALLENGE: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 501
    public static const HUKS_TAG_IS_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 1001
    public static const HUKS_TAG_KEY_STORAGE_FLAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 1002
    public static const HUKS_TAG_IS_ALLOWED_WRAP: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 1003
    public static const HUKS_TAG_KEY_WRAP_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 1004
    public static const HUKS_TAG_KEY_AUTH_ID: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 1005
    public static const HUKS_TAG_KEY_FLAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 1007
    public static const HUKS_TAG_KEY: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 10006
    public static const HUKS_TAG_AE_TAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 10009
}
```

**Description:** Represents tags for API call parameters.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_AE_TAG

```cangjie
public static const HUKS_TAG_AE_TAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 10009
```

**Description:** Field used to pass AEAD data in GCM mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_AGREE_ALG

```cangjie
public static const HUKS_TAG_AGREE_ALG: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 19
```

**Description:** Indicates the algorithm type during key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_AGREE_PRIVATE_KEY_ALIAS

```cangjie
public static const HUKS_TAG_AGREE_PRIVATE_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 21
```

**Description:** Indicates the private key alias during key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_AGREE_PUBLIC_KEY

```cangjie
public static const HUKS_TAG_AGREE_PUBLIC_KEY: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 22
```

**Description:** Indicates the public key during key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_AGREE_PUBLIC_KEY_IS_KEY_ALIAS

```cangjie
public static const HUKS_TAG_AGREE_PUBLIC_KEY_IS_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 20
```

**Description:** Indicates the public key alias during key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_ALGORITHM

```cangjie
public static const HUKS_TAG_ALGORITHM: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 1
```

**Description:** Represents the algorithm tag.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21### static const HUKS_TAG_ASSOCIATED_DATA

```cangjie
public static const HUKS_TAG_ASSOCIATED_DATA: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 8
```

**Description:** Represents the tag for additional authenticated data.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_ATTESTATION_CHALLENGE

```cangjie
public static const HUKS_TAG_ATTESTATION_CHALLENGE: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 501
```

**Description:** Represents the challenge value during attestation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_AUTH_TIMEOUT

```cangjie
public static const HUKS_TAG_AUTH_TIMEOUT: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 305
```

**Description:** Represents the single-use validity period of an auth token.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_AUTH_TOKEN

```cangjie
public static const HUKS_TAG_AUTH_TOKEN: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 306
```

**Description:** Field used to pass the auth token.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_BLOCK_MODE

```cangjie
public static const HUKS_TAG_BOCK_MODE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 6
```

**Description:** Represents the tag for encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_CHALLENGE_POS

```cangjie
public static const HUKS_TAG_CHALLENGE_POS: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 310
```

**Description:** When the challenge type is user-defined, the effective length of the challenge generated by Huks is only 8 bytes of consecutive data. Selected from [HuksChallengePosition](#class-hukschallengeposition).

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_CHALLENGE_TYPE

```cangjie
public static const HUKS_TAG_CHALLENGE_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 309
```

**Description:** Represents the type of challenge generated during key usage. Selected from [HuksChallengeType](#class-hukschallengetype).

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_DERIVE_KEY_SIZE

```cangjie
public static const HUKS_TAG_DERIVE_KEY_SIZE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 24
```

**Description:** Represents the size of the derived key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG

```cangjie
public static const HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 29
```

**Description:** Represents the storage type of derived/agreed keys.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_DIGEST

```cangjie
public static const HUKS_TAG_DIGEST: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 4
```

**Description:** Represents the tag for digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_IMPORT_KEY_TYPE

```cangjie
public static const HUKS_TAG_IMPORT_KEY_TYPE: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 25
```

**Description:** Represents the type of imported key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_INFO

```cangjie
public static const HUKS_TAG_INFO: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 11
```

**Description:** Represents the info parameter during key derivation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_IS_ALLOWED_WRAP

```cangjie
public static const HUKS_TAG_IS_ALLOWED_WRAP: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 1003
```

**Description:** Reserved.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_IS_KEY_ALIAS

```cangjie
public static const HUKS_TAG_IS_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 1001
```

**Description:** Indicates whether to use the alias passed during key generation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_ITERATION

```cangjie
public static const HUKS_TAG_ITERATION: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 14
```

**Description:** Represents the iteration count during key derivation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_IV

```cangjie
public static const HUKS_TAG_IV: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 10
```

**Description:** Represents the initialization vector for key operations.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY

```cangjie
public static const HUKS_TAG_KEY: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 10006
```

**Description:** Reserved.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY_ALIAS

```cangjie
public static const HUKS_TAG_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 23
```

**Description:** Represents the key alias.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY_AUTH_ACCESS_TYPE

```cangjie
public static const HUKS_TAG_KEY_AUTH_ACCESS_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 307
```

**Description:** Represents the secure access control type. Selected from [HuksAuthAccessType](#class-huksauthaccesstype). Must be set together with user authentication type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY_AUTH_ID

```cangjie
public static const HUKS_TAG_KEY_AUTH_ID: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 1005
```

**Description:** Reserved.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY_AUTH_PURPOSE

```cangjie
public static const HUKS_TAG_KEY_AUTH_PURPOSE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 311
```

**Description:** Represents the tag for key authentication purpose.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY_FLAG

```cangjie
public static const HUKS_TAG_KEY_FLAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 1007
```

**Description:** Represents the tag for key flags.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY_GENERATE_TYPE

```cangjie
public static const HUKS_TAG_KEY_GENERATE_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 15
```

**Description:** Represents the tag for key generation type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY_SECURE_SIGN_TYPE

```cangjie
public static const HUKS_TAG_KEY_SECURE_SIGN_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 308
```

**Description:** Specifies the signature type of the key during generation or import.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY_SIZE

```cangjie
public static const HUKS_TAG_KEY_SIZE: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 3
```

**Description:** Represents the tag for key length.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY_STORAGE_FLAG

```cangjie
public static const HUKS_TAG_KEY_STORAGE_FLAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 1002
```

**Description:** Represents the tag for key storage method.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY_TYPE

```cangjie
public static const HUKS_TAG_KEY_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 7
```

**Description:** Represents the tag for key type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_KEY_WRAP_TYPE

```cangjie
public static const HUKS_TAG_KEY_WRAP_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 1004
```

**Description:** Reserved.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_NO_AUTH_REQUIRED

```cangjie
public static const HUKS_TAG_NO_AUTH_REQUIRED: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 303
```

**Description:** Reserved.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21### static const HUKS_TAG_NONCE

```cangjie
public static const HUKS_TAG_NONCE: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 9
```

**Function:** Represents the NONCE field for key encryption/decryption.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_PADDING

```cangjie
public static const HUKS_TAG_PADDING: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 5
```

**Function:** Represents the tag for padding algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_PURPOSE

```cangjie
public static const HUKS_TAG_PURPOSE: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 2
```

**Function:** Represents the tag for key purpose.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_RSA_PSS_SALT_LEN_TYPE

```cangjie
public static const HUKS_TAG_RSA_PSS_SALT_LEN_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 30
```

**Function:** Represents the type of rsa_pss_salt_length.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_SALT

```cangjie
public static const HUKS_TAG_SALT: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 12
```

**Function:** Represents the salt value for key derivation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_UNWRAP_ALGORITHM_SUITE

```cangjie
public static const HUKS_TAG_UNWRAP_ALGORITHM_SUITE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 26
```

**Function:** Represents the suite for importing encrypted keys.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_USER_AUTH_TYPE

```cangjie
public static const HUKS_TAG_USER_AUTH_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 304
```

**Function:** Represents the user authentication type. Selected from [HuksUserAuthType](#class-huksuserauthtype), must be set together with secure access control type. Supports specifying two user authentication types simultaneously. For example: when secure access control type is specified as HUKS_SECURE_ACCESS_INVALID_NEW_BIO_ENROLL, the key access authentication type can be one of the following three: HUKS_USER_AUTH_TYPE_FACE, HUKS_USER_AUTH_TYPE_FINGERPRINT, HUKS_USER_AUTH_TYPE_FACE MagIc_StrINg HUKS_USER_AUTH_TYPE_FINGERPRINT.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_USER_ID

```cangjie
public static const HUKS_TAG_USER_ID: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 302
```

**Function:** Indicates which userID the current key belongs to.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21

### static const HUKS_TAG_AUTH_STORAGE_LEVEL

```cangjie
public static const HUKS_TAG_AUTH_STORAGE_LEVEL: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 316
```

**Function:** Security level for key storage, i.e., a value of HuksAuthStorageLevel.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 21