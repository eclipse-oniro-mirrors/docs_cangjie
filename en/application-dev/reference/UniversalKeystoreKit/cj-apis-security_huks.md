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
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration is needed in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## func abortSession(HuksHandleId, HuksOptions)

```cangjie
public func abortSession(handle: HuksHandleId, options: HuksOptions): Unit
```

**Description:** Interface for aborting key operations.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| handle | [HuksHandleId](#class-hukshandleid) | Yes | - | The handle for abortSession operation. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Parameter collection for abortSession operation. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | argument is invalid |
  | 801 | api is not supported |
  | 12000004 | operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | error occurred in crypto engine |
  | 12000012 | external error |
  | 12000014 | memory is insufficient |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.UniversalKeystoreKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let keyAlias = "KEY_ALIAS" // Key alias, specified during key generation and used for encryption, decryption, and key deletion
    let options = HuksOptions(properties:
        [
            HuksParam(HuksTag.HUKS_TAG_ALGORITHM, Uint32Value(HuksKeyAlg.HUKS_ALG_AES)),
            HuksParam(HuksTag.HUKS_TAG_KEY_SIZE, Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_128)),
            HuksParam(
                HuksTag.HUKS_TAG_PURPOSE,
                Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT)
            )
        ]
    )

    generateKeyItem(keyAlias, options)

    // encrypt and abort
    let handle = initSession(keyAlias, options).handle

    abortSession(handle, options)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func anonAttestKeyItem(String, HuksOptions)

```cangjie
public func anonAttestKeyItem(keyAlias: String, options: HuksOptions): Array<String>
```

**Description:** Obtains an anonymized key certificate. This operation requires network connectivity and may take a long time.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | Key alias, storing the alias of the key for which the certificate is to be obtained. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Specifies required parameters and data when obtaining the certificate. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | Returns the key certificate chain. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | check permission failed |
  | 401 | argument is invalid |
  | 801 | api is not supported |
  | 12000001 | algorithm mode is not supported |
  | 12000002 | algorithm param is missing |
  | 12000003 | algorithm param is invalid |
  | 12000004 | operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | error occurred in crypto engine |
  | 12000011 | queried entity does not exist |
  | 12000012 | external error |
  | 12000014 | memory is insufficient |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.UniversalKeystoreKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let keyAlias = "KEY_ALIAS" // Key alias, specified during key generation and used for encryption, decryption, and key deletion
    // generate key
    generateKeyItem(
        keyAlias,
        HuksOptions(properties:
            [
                HuksParam(HuksTag.HUKS_TAG_ALGORITHM, Uint32Value(HuksKeyAlg.HUKS_ALG_RSA)),
                HuksParam(HuksTag.HUKS_TAG_KEY_SIZE, Uint32Value(HuksKeySize.HUKS_RSA_KEY_SIZE_2048)),
                HuksParam(HuksTag.HUKS_TAG_PURPOSE, Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY)),
                HuksParam(HuksTag.HUKS_TAG_DIGEST, Uint32Value(HuksKeyDigest.HUKS_DIGEST_SHA256)),
                HuksParam(HuksTag.HUKS_TAG_PADDING, Uint32Value(HuksKeyPadding.HUKS_PADDING_PSS)),
                HuksParam(HuksTag.HUKS_TAG_BLOCK_MODE, Uint32Value(HuksCipherMode.HUKS_MODE_ECB))
            ]
        )
    )

    let challenge = "hi_challenge_data"
    let chains = anonAttestKeyItem(
        keyAlias,
        HuksOptions(properties:
            [
                HuksParam(HuksTag.HUKS_TAG_ATTESTATION_CHALLENGE, HuksParamValue.BytesValue(challenge.toArray())),
                HuksParam(HuksTag.HUKS_TAG_KEY_ALIAS, HuksParamValue.BytesValue(keyAlias.toArray()))
            ]
        )
    )
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func deleteKeyItem(String, HuksOptions)

```cangjie
public func deleteKeyItem(keyAlias: String, options: HuksOptions): Unit
```

**Description:** Deletes a key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | Key alias, which should be the same as the alias used during key generation. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Specifies the attribute Tag for the key to be deleted, such as the deletion scope (full/single). When deleting a single key, the Tag field can be left empty. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | argument is invalid |
  | 801 | api is not supported |
  | 12000004 | operating file failed |
  | 12000005 | IPC communication failed |
  | 12000011 | queried entity does not exist |
  | 12000012 | external error |
  | 12000014 | memory is insufficient |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.UniversalKeystoreKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    func generateSimpleKey(keyAlias: String) {
        let options = HuksOptions(properties:
            [
                HuksParam(HuksTag.HUKS_TAG_ALGORITHM, Uint32Value(HuksKeyAlg.HUKS_ALG_AES)),
                HuksParam(HuksTag.HUKS_TAG_KEY_SIZE, Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_128)),
                HuksParam(
                    HuksTag.HUKS_TAG_PURPOSE,
                    Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT)
                )
            ]
        )
        generateKeyItem(keyAlias, options)
    }

    func test_delete_key() {
        let keyAlias = "KEY_ALIAS" // Key alias, specified during key generation and used for encryption, decryption, and key deletion
        generateSimpleKey(keyAlias)
        // delete
        deleteKeyItem(keyAlias, HuksOptions())
    }

    test_delete_key()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func exportKeyItem(String, HuksOptions)

```cangjie
public func exportKeyItem(keyAlias: String, _: HuksOptions): Bytes
```

**Description:** Exports a key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | Key alias, which should be the same as the alias used during key generation. |
| _ | [HuksOptions](#class-huksoptions) | Yes | - | Empty object (pass empty here). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bytes | Returns the public key exported from the key. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | argument is invalid |
  | 801 | api is not supported |
  | 12000001 | algorithm mode is not supported |
  | 12000002 | algorithm param is missing |
  | 12000003 | algorithm param is invalid |
  | 12000004 | operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | error occurred in crypto engine |
  | 12000011 | queried entity does not exist |
  | 12000012 | external error |
  | 12000014 | memory is insufficient |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.UniversalKeystoreKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let keyAlias = "KEY_ALIAS" // Key alias, specified during key generation and used for encryption, decryption, and key deletion
    /* 1. Generate Key */
    generateKeyItem(
        keyAlias,
        HuksOptions(properties:
            [
                HuksParam(HuksTag.HUKS_TAG_ALGORITHM, Uint32Value(HuksKeyAlg.HUKS_ALG_ECC)),
                HuksParam(HuksTag.HUKS_TAG_KEY_SIZE, Uint32Value(HuksKeySize.HUKS_ECC_KEY_SIZE_256)),
                HuksParam(
                    HuksTag.HUKS_TAG_PURPOSE,
                    Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY | HuksKeyPurpose.HUKS_KEY_PURPOSE_SIGN
                )),
                HuksParam(HuksTag.HUKS_TAG_DIGEST, Uint32Value(HuksKeyDigest.HUKS_DIGEST_SHA256))
            ]
        )
    )
    /* 2. Export Key */
    let data = exportKeyItem(keyAlias, HuksOptions())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func finishSession(HuksHandleId, HuksOptions, Bytes)

```cangjie
public func finishSession(handle: HuksHandleId, options: HuksOptions, token!: Bytes): Option<Bytes>
```

**Description:** Interface for finishing key operations. [security_huks.initSession](#func-initsessionstring-huksoptions), [security_huks.updateSession](#func-updatesessionhukshandleid-huksoptions-bytes), and [security_huks.finishSession](#func-finishsessionhukshandleid-huksoptions-bytes) are three-stage interfaces that must be used together.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| handle | [HuksHandleId](#class-hukshandleid) | Yes | - | The handle for finishSession operation. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Parameter collection for finishSession operation. |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.UniversalKeystoreKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let keyAlias = "KEY_ALIAS" // Key alias, specified during key generation and used for encryption, decryption, and key deletion
    let options = HuksOptions(properties:
        [
            HuksParam(HuksTag.HUKS_TAG_ALGORITHM, Uint32Value(HuksKeyAlg.HUKS_ALG_AES)),
            HuksParam(HuksTag.HUKS_TAG_KEY_SIZE, Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_128)),
            HuksParam(
                HuksTag.HUKS_TAG_PURPOSE,
                Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT)
            ),
            HuksParam(HuksTag.HUKS_TAG_PADDING, Uint32Value(HuksKeyPadding.HUKS_PADDING_PKCS7)),
            HuksParam(HuksTag.HUKS_TAG_BOCK_MODE, Uint32Value(HuksCipherMode.HUKS_MODE_CBC))
        ]
    )
    generateKeyItem(keyAlias, options)
    // encrypt
    let handle = initSession(keyAlias, options).handle
    let cipherData = finishSession(handle, options)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
``````markdown
## func generateKeyItem(String, HuksOptions)

```cangjie
public func generateKeyItem(keyAlias: String, options: HuksOptions): Unit
```

**Function:** Generate a cryptographic key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | Key alias. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Contains tags required for key generation. Algorithm, key purpose, and key length are mandatory parameters. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | argument is invalid |
  | 801 | api is not supported |
  | 12000001 | algorithm mode is not supported |
  | 12000002 | algorithm param is missing |
  | 12000003 | algorithm param is invalid |
  | 12000004 | operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | error occurred in crypto engine |
  | 12000012 | external error |
  | 12000013 | queried credential does not exist |
  | 12000014 | memory is insufficient |
  | 12000015 | call service failed |
  | 12000017 | The key with same alias already exists |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.UniversalKeystoreKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let keyAlias = "KEY_ALIAS" // Key alias specified during key generation, used for encryption, decryption, and key deletion
    let options = HuksOptions(properties:
        [
            HuksParam(HuksTag.HUKS_TAG_ALGORITHM, Uint32Value(HuksKeyAlg.HUKS_ALG_AES)),
            HuksParam(HuksTag.HUKS_TAG_KEY_SIZE, Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_128)),
            HuksParam(
                HuksTag.HUKS_TAG_PURPOSE,
                Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT)
            )
        ]
    )
    generateKeyItem(keyAlias, options)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func getKeyItemProperties(String, HuksOptions)

```cangjie
public func getKeyItemProperties(keyAlias: String, _: HuksOptions): Array<HuksParam>
```

**Function:** Retrieve key properties.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | Key alias. |
| _ | [HuksOptions](#class-huksoptions) | Yes | - | Empty object (pass empty here). |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[HuksParam](#class-huksparam)> | Returns key properties. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | argument is invalid |
  | 801 | api is not supported |
  | 12000001 | algorithm mode is not supported |
  | 12000002 | algorithm param is missing |
  | 12000003 | algorithm param is invalid |
  | 12000004 | operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | error occurred in crypto engine |
  | 12000011 | queried entity does not exist |
  | 12000012 | external error |
  | 12000014 | memory is insufficient |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.UniversalKeystoreKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let keyAlias = "KEY_ALIAS" // Key alias specified during key generation, used for encryption, decryption, and key deletion
    let options = HuksOptions(properties:
        [
            HuksParam(HuksTag.HUKS_TAG_ALGORITHM, Uint32Value(HuksKeyAlg.HUKS_ALG_AES)),
            HuksParam(HuksTag.HUKS_TAG_KEY_SIZE, Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_128)),
            HuksParam(
                HuksTag.HUKS_TAG_PURPOSE,
                Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT)
            )
        ]
    )
    let properties = getKeyItemProperties(keyAlias, HuksOptions())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func importKeyItem(String, HuksOptions)

```cangjie
public func importKeyItem(keyAlias: String, options: HuksOptions): Unit
```

**Function:** Import a plaintext key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | Key alias. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Contains tags required for key import and the key to be imported. Algorithm, key purpose, and key length are mandatory parameters. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | argument is invalid |
  | 801 | api is not supported |
  | 12000001 | algorithm mode is not supported |
  | 12000002 | algorithm param is missing |
  | 12000003 | algorithm param is invalid |
  | 12000004 | operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | error occurred in crypto engine |
  | 12000011 | queried entity does not exist |
  | 12000012 | external error |
  | 12000013 | queried credential does not exist |
  | 12000014 | memory is insufficient |
  | 12000015 | call service failed |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.UniversalKeystoreKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let keyAlias = "KEY_ALIAS" // Key alias specified during key generation, used for encryption, decryption, and key deletion
    let key = Array<UInt8>(Int64(HuksKeySize.HUKS_AES_KEY_SIZE_256 / 8), 
    {i => UInt8(i & 0xFF)})
    importKeyItem(
        keyAlias,
        HuksOptions(properties:
            [
                HuksParam(HuksTag.HUKS_TAG_ALGORITHM, Uint32Value(HuksKeyAlg.HUKS_ALG_AES)),
                HuksParam(HuksTag.HUKS_TAG_KEY_SIZE, Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_256)),
                HuksParam(
                    HuksTag.HUKS_TAG_PURPOSE,
                    Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT)
                )
            ],
            inData: key
        )
    )
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func importWrappedKeyItem(String, String, HuksOptions)

```cangjie
public func importWrappedKeyItem(keyAlias: String, wrappingKeyAlias: String, options: HuksOptions): Unit
```

**Function:** Import an encrypted key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | Key alias for storing the imported key. |
| wrappingKeyAlias | String | Yes | - | Key alias corresponding to the key used for decrypting the encrypted key data. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Contains tags required for key import and the encrypted key data to be imported. Algorithm, key purpose, and key length are mandatory parameters. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | check permission failed |
  | 401 | argument is invalid |
  | 801 | api is not supported |
  | 12000001 | algorithm mode is not supported |
  | 12000002 | algorithm param is missing |
  | 12000003 | algorithm param is invalid |
  | 12000004 | operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | error occurred in crypto engine |
  | 12000011 | queried entity does not exist |
  | 12000012 | external error |
  | 12000013 | queried credential does not exist |
  | 12000014 | memory is insufficient |
  | 12000015 | call service failed |
  | 12000017 | The key with same alias already exists |

## func initSession(String, HuksOptions)

```cangjie
public func initSession(keyAlias: String, options: HuksOptions): HuksSessionHandle
```

**Function:** Initialize a session for key operations. [security_huks.initSession](#func-initsessionstring-huksoptions), [security_huks.updateSession](#func-updatesessionhukshandleid-huksoptions-bytes), and [security_huks.finishSession](#func-finishsessionhukshandleid-huksoptions-bytes) are three-phase APIs that must be used together.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | Key alias for initializing the session. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Parameter set for initializing the session. |

**Return Value:**

| Type | Description |
|:----|:----|
| [HuksSessionHandle](#class-hukssessionhandle) | Returns the HUKS session handle. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | argument is invalid |
  | 801 | api is not supported |
  | 12000001 | algorithm mode is not supported |
  | 12000002 | algorithm param is missing |
  | 12000003 | algorithm param is invalid |
  | 12000004 | operating file failed |
  | 12000005 | IPC communication failed |
  | 12000006 | error occurred in crypto engine |
  | 12000010 | the number of sessions has reached limit |
  | 12000011 | queried entity does not exist |
  | 12000012 | external error |
  | 12000014 | memory is insufficient |
  | 12000018 | the input parameter is invalid |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.UniversalKeystoreKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let keyAlias = "KEY_ALIAS" // Key alias specified during key generation, used for encryption, decryption, and key deletion
    let options = HuksOptions(properties:
        [
            HuksParam(HuksTag.HUKS_TAG_ALGORITHM, Uint32Value(HuksKeyAlg.HUKS_ALG_AES)),
            HuksParam(HuksTag.HUKS_TAG_KEY_SIZE, Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_128)),
            HuksParam(
                HuksTag.HUKS_TAG_PURPOSE,
                Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT)
            ),
            HuksParam(HuksTag.HUKS_TAG_PADDING, Uint32Value(HuksKeyPadding.HUKS_PADDING_PKCS7)),
            HuksParam(HuksTag.HUKS_TAG_BOCK_MODE, Uint32Value(HuksCipherMode.HUKS_MODE_CBC))
        ]
    )
    generateKeyItem(keyAlias, options)
    // encrypt
    let handle = initSession(keyAlias, encOptions).handle
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func hasKeyItemExist(String, HuksOptions)

```cangjie
public func hasKeyItemExist(keyAlias: String, options: HuksOptions): Bool
```

**Function:** Check if a key exists.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyAlias | String | Yes | - | Key alias to be checked. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Specifies the attribute tags for querying the key, such as query scope (all/single). For single queries, the tag field can be empty. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Indicates whether the key exists. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [HUKS Error Codes](./cj-errorcode-huks.md) and [Universal Error Codes](../cj-errorcode-universal.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.UniversalKeystoreKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to dependency definitions
    func generateSimpleKey(keyAlias: String) {
        let options = HuksOptions(properties:
            [
                HuksParam(HuksTag.HUKS_TAG_ALGORITHM, Uint32Value(HuksKeyAlg.HUKS_ALG_AES)),
                HuksParam(HuksTag.HUKS_TAG_KEY_SIZE, Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_128)),
                HuksParam(
                    HuksTag.HUKS_TAG_PURPOSE,
                    Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_ENCRYPT | HuksKeyPurpose.HUKS_KEY_PURPOSE_DECRYPT)
                )
            ]
        )
        generateKeyItem(keyAlias, options)
    }

    let keyAlias = "KEY_ALIAS" // Key alias specified during key generation, used for encryption, decryption, and key deletion
    hasKeyItemExist(keyAlias, HuksOptions()) // false
    generateSimpleKey(keyAlias)
    hasKeyItemExist(keyAlias, HuksOptions()) // true
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
``````markdown
## func updateSession(HuksHandleId, HuksOptions, Bytes)

```cangjie
public func updateSession(handle: HuksHandleId, options: HuksOptions, token!: Bytes): Option<Bytes>
```

**Function:** The updateSession operation for key interfaces. [security_huks.initSession](#func-initsessionstring-huksoptions), [security_huks.updateSession](#func-updatesessionhukshandleid-huksoptions-bytes), and [security_huks.finishSession](#func-finishsessionhukshandleid-huksoptions-bytes) form a three-stage interface that must be used together.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| handle | [HuksHandleId](#class-hukshandleid) | Yes | - | The handle for the updateSession operation. |
| options | [HuksOptions](#class-huksoptions) | Yes | - | Parameter set for updateSession. |
| token | Bytes | No | Bytes\<UInt8>() | Represents the AuthToken value from USER IAM service. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<Bytes> | Outputs the key update result. |

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

## class HuksAuthAccessType

```cangjie
public class HuksAuthAccessType {
    public static const HUKS_AUTH_ACCESS_INVALID_CLEAR_PASSWORD: UInt32 = 1 << 0
    public static const HUKS_AUTH_ACCESS_INVALID_NEW_BIO_ENROLL: UInt32 = 1 << 1
}
```

**Function:** Represents security access control types.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_AUTH_ACCESS_INVALID_CLEAR_PASSWORD

```cangjie
public static const HUKS_AUTH_ACCESS_INVALID_CLEAR_PASSWORD: UInt32 = 1 << 0
```

**Function:** Indicates that the security access control type is "this key is always valid."

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_AUTH_ACCESS_INVALID_NEW_BIO_ENROLL

```cangjie
public static const HUKS_AUTH_ACCESS_INVALID_NEW_BIO_ENROLL: UInt32 = 1 << 1
```

**Function:** Indicates that the security access control type is "key becomes invalid after password clearance."

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

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

**Since:** 22

### static const HUKS_AUTH_STORAGE_LEVEL_CE

```cangjie
public static const HUKS_AUTH_STORAGE_LEVEL_CE: UInt32 = 1
```

**Function:** Indicates the key is accessible only after the first unlock.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_AUTH_STORAGE_LEVEL_DE

```cangjie
public static const HUKS_AUTH_STORAGE_LEVEL_DE: UInt32 = 0
```

**Function:** Indicates the key is accessible only after boot.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_AUTH_STORAGE_LEVEL_ECE

```cangjie
public static const HUKS_AUTH_STORAGE_LEVEL_ECE: UInt32 = 2
```

**Function:** Indicates the key is accessible only in the unlocked state.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

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

**Since:** 22

### static const HUKS_CHALLENGE_POS_0

```cangjie
public static const HUKS_CHALLENGE_POS_0: UInt32 = 0
```

**Function:** Indicates bytes 0-7 are the valid challenge for the current key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_CHALLENGE_POS_1

```cangjie
public static const HUKS_CHALLENGE_POS_1: UInt32 = 1
```

**Function:** Indicates bytes 8-15 are the valid challenge for the current key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_CHALLENGE_POS_2

```cangjie
public static const HUKS_CHALLENGE_POS_2: UInt32 = 2
```

**Function:** Indicates bytes 16-23 are the valid challenge for the current key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_CHALLENGE_POS_3

```cangjie
public static const HUKS_CHALLENGE_POS_3: UInt32 = 3
```

**Function:** Indicates bytes 24-31 are the valid challenge for the current key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

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

**Since:** 22

### static const HUKS_CHALLENGE_TYPE_CUSTOM

```cangjie
public static const HUKS_CHALLENGE_TYPE_CUSTOM: UInt32 = 1
```

**Function:** Indicates a user-defined challenge type. Supports single authentication for multiple keys.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_CHALLENGE_TYPE_NONE

```cangjie
public static const HUKS_CHALLENGE_TYPE_NONE: UInt32 = 2
```

**Function:** Indicates a no-challenge type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_CHALLENGE_TYPE_NORMAL

```cangjie
public static const HUKS_CHALLENGE_TYPE_NORMAL: UInt32 = 0
```

**Function:** Indicates a normal challenge type, defaulting to 32 bytes.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

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

**Since:** 22

### static const HUKS_MODE_CBC

```cangjie
public static const HUKS_MODE_CBC: UInt32 = 2
```

**Function:** Indicates CBC encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_MODE_CCM

```cangjie
public static const HUKS_MODE_CCM: UInt32 = 31
```

**Function:** Indicates CCM encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_MODE_CTR

```cangjie
public static const HUKS_MODE_CTR: UInt32 = 3
```

**Function:** Indicates CTR encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_MODE_ECB

```cangjie
public static const HUKS_MODE_ECB: UInt32 = 1
```

**Function:** Indicates ECB encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_MODE_GCM

```cangjie
public static const HUKS_MODE_GCM: UInt32 = 32
```

**Function:** Indicates GCM encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_MODE_OFB

```cangjie
public static const HUKS_MODE_OFB: UInt32 = 4
```

**Function:** Indicates OFB encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

## class HuksHandleId

```cangjie
public class HuksHandleId {}
```

**Function:** Represents the ID of an encryption handle.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

## class HuksImportKeyType

```cangjie
public class HuksImportKeyType {
    public static const HUKS_KEY_TYPE_PUBLIC_KEY: UInt32 = 0
    public static const HUKS_KEY_TYPE_PRIVATE_KEY: UInt32 = 1
    public static const HUKS_KEY_TYPE_KEY_PAIR: UInt32 = 2
}
```

**Function:** Specifies the type of key being imported. Defaults to public key. Not required for symmetric key imports.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_TYPE_KEY_PAIR

```cangjie
public static const HUKS_KEY_TYPE_KEY_PAIR: UInt32 = 2
```

**Function:** Indicates the imported key type is a public-private key pair.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_TYPE_PRIVATE_KEY

```cangjie
public static const HUKS_KEY_TYPE_PRIVATE_KEY: UInt32 = 1
```

**Function:** Indicates the imported key type is a private key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_TYPE_PUBLIC_KEY

```cangjie
public static const HUKS_KEY_TYPE_PUBLIC_KEY: UInt32 = 0
```

**Function:** Indicates the imported key type is a public key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22
```## class HuksKeyAlg

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

**Function:** Represents the algorithm used by the key.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_AES

```cangjie
public static const HUKS_ALG_AES: UInt32 = 20
```

**Function:** Represents the AES algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_DH

```cangjie
public static const HUKS_ALG_DH: UInt32 = 103
```

**Function:** Represents the DH algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_DSA

```cangjie
public static const HUKS_ALG_DSA: UInt32 = 3
```

**Function:** Represents the DSA algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_ECC

```cangjie
public static const HUKS_ALG_ECC: UInt32 = 2
```

**Function:** Represents the ECC algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_ECDH

```cangjie
public static const HUKS_ALG_ECDH: UInt32 = 100
```

**Function:** Represents the ECDH algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_ED25519

```cangjie
public static const HUKS_ALG_ED25519: UInt32 = 102
```

**Function:** Represents the ED25519 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_HKDF

```cangjie
public static const HUKS_ALG_HKDF: UInt32 = 51
```

**Function:** Represents the HKDF algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_HMAC

```cangjie
public static const HUKS_ALG_HMAC: UInt32 = 50
```

**Function:** Represents the HMAC algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_PBKDF2

```cangjie
public static const HUKS_ALG_PBKDF2: UInt32 = 52
```

**Function:** Represents the PBKDF2 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_RSA

```cangjie
public static const HUKS_ALG_RSA: UInt32 = 1
```

**Function:** Represents the RSA algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_SM2

```cangjie
public static const HUKS_ALG_SM2: UInt32 = 150
```

**Function:** Represents the SM2 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_SM3

```cangjie
public static const HUKS_ALG_SM3: UInt32 = 151
```

**Function:** Represents the SM3 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_SM4

```cangjie
public static const HUKS_ALG_SM4: UInt32 = 152
```

**Function:** Represents the SM4 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ALG_X25519

```cangjie
public static const HUKS_ALG_X25519: UInt32 = 101
```

**Function:** Represents the X25519 algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

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

**Function:** Represents the digest algorithm.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_DIGEST_MD5

```cangjie
public static const HUKS_DIGEST_MD5: UInt32 = 1
```

**Function:** Represents the MD5 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_DIGEST_NONE

```cangjie
public static const HUKS_DIGEST_NONE: UInt32 = 0
```

**Function:** Represents no digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_DIGEST_SHA1

```cangjie
public static const HUKS_DIGEST_SHA1: UInt32 = 10
```

**Function:** Represents the SHA1 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_DIGEST_SHA224

```cangjie
public static const HUKS_DIGEST_SHA224: UInt32 = 11
```

**Function:** Represents the SHA224 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_DIGEST_SHA256

```cangjie
public static const HUKS_DIGEST_SHA256: UInt32 = 12
```

**Function:** Represents the SHA256 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_DIGEST_SHA384

```cangjie
public static const HUKS_DIGEST_SHA384: UInt32 = 13
```

**Function:** Represents the SHA384 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_DIGEST_SHA512

```cangjie
public static const HUKS_DIGEST_SHA512: UInt32 = 14
```

**Function:** Represents the SHA512 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_DIGEST_SM3

```cangjie
public static const HUKS_DIGEST_SM3: UInt32 = 2
```

**Function:** Represents the SM3 digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

## class HuksKeyFlag

```cangjie
public class HuksKeyFlag {
    public static const HUKS_KEY_FLAG_IMPORT_KEY: UInt32 = 1
    public static const HUKS_KEY_FLAG_GENERATE_KEY: UInt32 = 2
    public static const HUKS_KEY_FLAG_AGREE_KEY: UInt32 = 3
    public static const HUKS_KEY_FLAG_DERIVE_KEY: UInt32 = 4
}
```

**Function:** Represents the method of key generation.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_FLAG_AGREE_KEY

```cangjie
public static const HUKS_KEY_FLAG_AGREE_KEY: UInt32 = 3
```

**Function:** Represents a key generated through the key agreement interface.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_FLAG_DERIVE_KEY

```cangjie
public static const HUKS_KEY_FLAG_DERIVE_KEY: UInt32 = 4
```

**Function:** Represents a key generated through the key derivation interface.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_FLAG_GENERATE_KEY

```cangjie
public static const HUKS_KEY_FLAG_GENERATE_KEY: UInt32 = 2
```

**Function:** Represents a key generated through the key generation interface.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_FLAG_IMPORT_KEY

```cangjie
public static const HUKS_KEY_FLAG_IMPORT_KEY: UInt32 = 1
```

**Function:** Represents a key imported through the public key import interface.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22## class HuksKeyGeneraterationType

```cangjie
public class HuksKeyGeneraterationType {
    public static const HUKS_KEY_GENERATE_TYPE_DEFAULT: UInt32 = 0
    public static const HUKS_KEY_GENERATE_TYPE_DERIVE: UInt32 = 1
    public static const HUKS_KEY_GENERATE_TYPE_AGREE: UInt32 = 2
}
```

**Description:** Represents the type of key generation.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_GENERATE_TYPE_AGREE

```cangjie
public static const HUKS_KEY_GENERATE_TYPE_AGREE: UInt32 = 2
```

**Description:** Key generated through agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_GENERATE_TYPE_DEFAULT

```cangjie
public static const HUKS_KEY_GENERATE_TYPE_DEFAULT: UInt32 = 0
```

**Description:** Default generated key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_GENERATE_TYPE_DERIVE

```cangjie
public static const HUKS_KEY_GENERATE_TYPE_DERIVE: UInt32 = 1
```

**Description:** Key generated through derivation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

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

**Description:** Represents padding algorithms.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_PADDING_NONE

```cangjie
public static const HUKS_PADDING_NONE: UInt32 = 0
```

**Description:** Indicates no padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_PADDING_OAEP

```cangjie
public static const HUKS_PADDING_OAEP: UInt32 = 1
```

**Description:** Indicates OAEP padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_PADDING_PKCS1_V1_5

```cangjie
public static const HUKS_PADDING_PKCS1_V1_5: UInt32 = 3
```

**Description:** Indicates PKCS1_V1_5 padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_PADDING_PKCS5

```cangjie
public static const HUKS_PADDING_PKCS5: UInt32 = 4
```

**Description:** Indicates PKCS5 padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_PADDING_PKCS7

```cangjie
public static const HUKS_PADDING_PKCS7: UInt32 = 5
```

**Description:** Indicates PKCS7 padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_PADDING_PSS

```cangjie
public static const HUKS_PADDING_PSS: UInt32 = 2
```

**Description:** Indicates PSS padding algorithm is used.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

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

**Description:** Represents key purposes.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_PURPOSE_AGREE

```cangjie
public static const HUKS_KEY_PURPOSE_AGREE: UInt32 = 256
```

**Description:** Indicates the key is used for key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_PURPOSE_DECRYPT

```cangjie
public static const HUKS_KEY_PURPOSE_DECRYPT: UInt32 = 2
```

**Description:** Indicates the key is used for decrypting ciphertext.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_PURPOSE_DERIVE

```cangjie
public static const HUKS_KEY_PURPOSE_DERIVE: UInt32 = 16
```

**Description:** Indicates the key is used for key derivation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_PURPOSE_ENCRYPT

```cangjie
public static const HUKS_KEY_PURPOSE_ENCRYPT: UInt32 = 1
```

**Description:** Indicates the key is used for encrypting plaintext.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_PURPOSE_MAC

```cangjie
public static const HUKS_KEY_PURPOSE_MAC: UInt32 = 128
```

**Description:** Indicates the key is used for generating MAC (Message Authentication Code).

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_PURPOSE_SIGN

```cangjie
public static const HUKS_KEY_PURPOSE_SIGN: UInt32 = 4
```

**Description:** Indicates the key is used for signing data.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_PURPOSE_UNWRAP

```cangjie
public static const HUKS_KEY_PURPOSE_UNWRAP: UInt32 = 64
```

**Description:** Indicates the key is used for encrypted import.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_PURPOSE_VERIFY

```cangjie
public static const HUKS_KEY_PURPOSE_VERIFY: UInt32 = 8
```

**Description:** Indicates the key is used for verifying signed data.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_KEY_PURPOSE_WRAP

```cangjie
public static const HUKS_KEY_PURPOSE_WRAP: UInt32 = 32
```

**Description:** Indicates the key is used for encrypted export.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

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

**Description:** Represents key sizes.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_AES_KEY_SIZE_128

```cangjie
public static const HUKS_AES_KEY_SIZE_128: UInt32 = 128
```

**Description:** Indicates AES algorithm key size is 128 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_AES_KEY_SIZE_192

```cangjie
public static const HUKS_AES_KEY_SIZE_192: UInt32 = 192
```

**Description:** Indicates AES algorithm key size is 192 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_AES_KEY_SIZE_256

```cangjie
public static const HUKS_AES_KEY_SIZE_256: UInt32 = 256
```

**Description:** Indicates AES algorithm key size is 256 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_CURVE25519_KEY_SIZE_256

```cangjie
public static const HUKS_CURVE25519_KEY_SIZE_256: UInt32 = 256
```

**Description:** Indicates CURVE25519 algorithm key size is 256 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_DH_KEY_SIZE_2048

```cangjie
public static const HUKS_DH_KEY_SIZE_2048: UInt32 = 2048
```

**Description:** Indicates DH algorithm key size is 2048 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_DH_KEY_SIZE_3072

```cangjie
public static const HUKS_DH_KEY_SIZE_3072: UInt32 = 3072
```

**Description:** Indicates DH algorithm key size is 3072 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_DH_KEY_SIZE_4096

```cangjie
public static const HUKS_DH_KEY_SIZE_4096: UInt32 = 4096
```

**Description:** Indicates DH algorithm key size is 4096 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ECC_KEY_SIZE_224

```cangjie
public static const HUKS_ECC_KEY_SIZE_224: UInt32 = 224
```

**Description:** Indicates ECC algorithm key size is 224 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ECC_KEY_SIZE_256

```cangjie
public static const HUKS_ECC_KEY_SIZE_256: UInt32 = 256
```

**Description:** Indicates ECC algorithm key size is 256 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ECC_KEY_SIZE_384

```cangjie
public static const HUKS_ECC_KEY_SIZE_384: UInt32 = 384
```

**Description:** Indicates ECC algorithm key size is 384 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_ECC_KEY_SIZE_521

```cangjie
public static const HUKS_ECC_KEY_SIZE_521: UInt32 = 521
```

**Description:** Indicates ECC algorithm key size is 521 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_RSA_KEY_SIZE_1024

```cangjie
public static const HUKS_RSA_KEY_SIZE_1024: UInt32 = 1024
```

**Description:** Indicates RSA algorithm key size is 1024 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_RSA_KEY_SIZE_2048

```cangjie
public static const HUKS_RSA_KEY_SIZE_2048: UInt32 = 2048
```

**Description:** Indicates RSA algorithm key size is 2048 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_RSA_KEY_SIZE_3072

```cangjie
public static const HUKS_RSA_KEY_SIZE_3072: UInt32 = 3072
```

**Description:** Indicates RSA algorithm key size is 3072 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_RSA_KEY_SIZE_4096

```cangjie
public static const HUKS_RSA_KEY_SIZE_4096: UInt32 = 4096
```

**Description:** Indicates RSA algorithm key size is 4096 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_RSA_KEY_SIZE_512

```cangjie
public static const HUKS_RSA_KEY_SIZE_512: UInt32 = 512
```

**Description:** Indicates RSA algorithm key size is 512 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_RSA_KEY_SIZE_768

```cangjie
public static const HUKS_RSA_KEY_SIZE_768: UInt32 = 768
```

**Description:** Indicates RSA algorithm key size is 768 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_SM2_KEY_SIZE_256

```cangjie
public static const HUKS_SM2_KEY_SIZE_256: UInt32 = 256
```

**Description:** Indicates SM2 algorithm key size is 256 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_SM4_KEY_SIZE_128

```cangjie
public static const HUKS_SM4_KEY_SIZE_128: UInt32 = 128
```

**Description:** Indicates SM4 algorithm key size is 128 bits.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22## class HuksKeyStorageType

```cangjie
public class HuksKeyStorageType {
    public static const HUKS_STORAGE_ONLY_USED_IN_HUKS: UInt32 = 2
    public static const HUKS_STORAGE_KEY_EXPORT_ALLOWED: UInt32 = 3
}
```

**Description:** Represents key storage methods.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_STORAGE_KEY_EXPORT_ALLOWED

```cangjie
public static const HUKS_STORAGE_KEY_EXPORT_ALLOWED: UInt32 = 3
```

**Description:** Indicates that the key derived from the master key can be directly exported to the business party, and HUKS does not provide hosting services for it.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_STORAGE_ONLY_USED_IN_HUKS

```cangjie
public static const HUKS_STORAGE_ONLY_USED_IN_HUKS: UInt32 = 2
```

**Description:** Indicates that the key derived from the master key is stored in HUKS and hosted by HUKS.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

## class HuksOptions

```cangjie
public class HuksOptions {
    public var properties: Array<HuksParam>
    public var inData: Bytes

    public init(properties!: Array<HuksParam> = Array<HuksParam>(), inData!: Bytes = Bytes())
}
```

**Description:** Options used for API calls.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### var inData

```cangjie
public var inData: Bytes
```

**Description:** Input data.

**Type:** Bytes

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### var properties

```cangjie
public var properties: Array<HuksParam>
```

**Description:** Properties, an array for storing HuksParam.

**Type:** Array\<[HuksParam](#class-huksparam)>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### init(Array\<HuksParam>, Bytes)

```cangjie

public init(properties!: Array<HuksParam> = Array<HuksParam>(), inData!: Bytes = Bytes())
```

**Description:** Constructs an instance of options for API calls.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|properties|Array\<[HuksParam](#class-huksparam)>|No|Array<HuksParam>()|Properties, an array for storing HuksParam.|
|inData|Bytes|No|Bytes\<UInt8>()|Input data.|

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

**Since:** 22

### var tag

```cangjie
public var tag: UInt32
```

**Description:** Tag.

**Type:** UInt32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### var value

```cangjie
public var value: HuksParamValue
```

**Description:** Value corresponding to the tag.

**Type:** UInt32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### init(UInt32, HuksParamValue)

```cangjie

public init(tag: UInt32, value: HuksParamValue)
```

**Description:** Constructs an instance of an element in the properties array of [HuksOptions](#class-huksoptions).

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|tag|UInt32|Yes|-|Tag.|
|value|[HuksParamValue](#enum-huksparamvalue)|Yes|-|Value corresponding to the tag.|

## class HuksRsaPssSaltLenType

```cangjie
public class HuksRsaPssSaltLenType {
    public static const HUKS_RSA_PSS_SALT_LEN_DIGEST: UInt32 = 0
    public static const HUKS_RSA_PSS_SALT_LEN_MAX: UInt32 = 1
}
```

**Description:** Represents the salt_len type that needs to be specified when RSA performs signing or verification with PSS padding.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_RSA_PSS_SALT_LEN_DIGEST

```cangjie
public static const HUKS_RSA_PSS_SALT_LEN_DIGEST: UInt32 = 0
```

**Description:** Indicates setting salt_len based on the digest length.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_RSA_PSS_SALT_LEN_MAX

```cangjie
public static const HUKS_RSA_PSS_SALT_LEN_MAX: UInt32 = 1
```

**Description:** Indicates setting salt_len based on the maximum length.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

## class HuksSecureSignType

```cangjie
public class HuksSecureSignType {
    public static const HUKS_SECURE_SIGN_WITH_AUTH_INFO: UInt32 = 1
}
```

**Description:** Represents the signature type specified when generating or importing a key.

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_SECURE_SIGN_WITH_AUTH_INFO

```cangjie
public static const HUKS_SECURE_SIGN_WITH_AUTH_INFO: UInt32 = 1
```

**Description:** Indicates the signature type carries authentication information. If this field is specified when generating or importing a key, authentication information will be added to the data to be signed before signing when using the key for signing.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

## class HuksSessionHandle

```cangjie
public class HuksSessionHandle {
    public var handle: HuksHandleId
    public var challenge: Bytes
}
```

**Description:** HUKS Handle structure.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### var challenge

```cangjie
public var challenge: Bytes
```

**Description:** Represents the challenge information obtained after the [initSession](#func-initsessionstring-huksoptions) operation.

**Type:** Bytes

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### var handle

```cangjie
public var handle: HuksHandleId
```

**Description:** Represents the handle value.

**Type:** [HuksHandleId](#class-hukshandleid)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

## class HuksTag

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
    public static const HUKS_TAG_KEY_GENERATION_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 15
    public static const HUKS_TAG_ALG_FOR_AGREEMENT: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 19
    public static const HUKS_TAG_AGREE_PUBLIC_KEY_IS_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 20
    public static const HUKS_TAG_PRIVATE_KEY_ALIAS_FOR_AGREEMENT: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 21
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

**Description:** Represents the tags for call parameters.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_AE_TAG

```cangjie
public static const HUKS_TAG_AE_TAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 10009
```

**Description:** Field used for passing AEAD data in GCM mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_ALG_FOR_AGREEMENT

```cangjie
public static const HUKS_TAG_ALG_FOR_AGREEMENT: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 19
```

**Description:** Represents the algorithm type for key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_PRIVATE_KEY_ALIAS_FOR_AGREEMENT

```cangjie
public static const HUKS_TAG_PRIVATE_KEY_ALIAS_FOR_AGREEMENT: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 21
```

**Description:** Represents the private key alias for key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_AGREE_PUBLIC_KEY

```cangjie
public static const HUKS_TAG_AGREE_PUBLIC_KEY: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 22
```

**Description:** Represents the public key for key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22### static const HUKS_TAG_AGREE_PUBLIC_KEY_IS_KEY_ALIAS

```cangjie
public static const HUKS_TAG_AGREE_PUBLIC_KEY_IS_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 20
```

**Description:** Indicates the alias of the public key during key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_ALGORITHM

```cangjie
public static const HUKS_TAG_ALGORITHM: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 1
```

**Description:** Represents the tag for algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_ASSOCIATED_DATA

```cangjie
public static const HUKS_TAG_ASSOCIATED_DATA: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 8
```

**Description:** Represents the tag for additional authenticated data.

**Type:** UInt32

**System Capability:**  SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_ATTESTATION_CHALLENGE

```cangjie
public static const HUKS_TAG_ATTESTATION_CHALLENGE: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 501
```

**Description:** Represents the challenge value during attestation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_TAG_AUTH_TIMEOUT

```cangjie
public static const HUKS_TAG_AUTH_TIMEOUT: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 305
```

**Description:** Indicates the single-use validity period of the auth token.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_TAG_AUTH_TOKEN

```cangjie
public static const HUKS_TAG_AUTH_TOKEN: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 306
```

**Description:** Field for passing the auth token.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_TAG_BLOCK_MODE

```cangjie
public static const HUKS_TAG_BLOCK_MODE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 6
```

**Description:** Represents the tag for encryption mode.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_CHALLENGE_POS

```cangjie
public static const HUKS_TAG_CHALLENGE_POS: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 310
```

**Description:** When the challenge type is user-defined, the effective length of the challenge generated by Huks is only 8 bytes of consecutive data. Selected from [HuksChallengePosition](#class-hukschallengeposition).

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_TAG_CHALLENGE_TYPE

```cangjie
public static const HUKS_TAG_CHALLENGE_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 309
```

**Description:** Indicates the type of challenge generated during key usage. Selected from [HuksChallengeType](#class-hukschallengetype).

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_TAG_DERIVE_KEY_SIZE

```cangjie
public static const HUKS_TAG_DERIVE_KEY_SIZE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 24
```

**Description:** Indicates the size of the derived key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG

```cangjie
public static const HUKS_TAG_DERIVED_AGREED_KEY_STORAGE_FLAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 29
```

**Description:** Indicates the storage type of the derived/agreed key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_DIGEST

```cangjie
public static const HUKS_TAG_DIGEST: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 4
```

**Description:** Represents the tag for digest algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_IMPORT_KEY_TYPE

```cangjie
public static const HUKS_TAG_IMPORT_KEY_TYPE: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 25
```

**Description:** Indicates the type of imported key.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_INFO

```cangjie
public static const HUKS_TAG_INFO: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 11
```

**Description:** Represents the info during key derivation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_IS_ALLOWED_WRAP

```cangjie
public static const HUKS_TAG_IS_ALLOWED_WRAP: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 1003
```

**Description:** Reserved.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_IS_KEY_ALIAS

```cangjie
public static const HUKS_TAG_IS_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 1001
```

**Description:** Indicates whether to use the alias passed during key generation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_ITERATION

```cangjie
public static const HUKS_TAG_ITERATION: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 14
```

**Description:** Indicates the iteration count during key derivation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_IV

```cangjie
public static const HUKS_TAG_IV: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 10
```

**Description:** Represents the initialization vector for key initialization.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_KEY

```cangjie
public static const HUKS_TAG_KEY: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 10006
```

**Description:** Reserved.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_KEY_ALIAS

```cangjie
public static const HUKS_TAG_KEY_ALIAS: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 23
```

**Description:** Represents the key alias.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_KEY_AUTH_ACCESS_TYPE

```cangjie
public static const HUKS_TAG_KEY_AUTH_ACCESS_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 307
```

**Description:** Indicates the secure access control type. Selected from [HuksAuthAccessType](#class-huksauthaccesstype), must be set together with user authentication type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_TAG_KEY_AUTH_ID

```cangjie
public static const HUKS_TAG_KEY_AUTH_ID: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 1005
```

**Description:** Reserved.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_TAG_KEY_AUTH_PURPOSE

```cangjie
public static const HUKS_TAG_KEY_AUTH_PURPOSE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 311
```

**Description:** Represents the tag for key authentication purpose.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_TAG_KEY_FLAG

```cangjie
public static const HUKS_TAG_KEY_FLAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 1007
```

**Description:** Represents the tag for key flag.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_KEY_GENERATION_TYPE

```cangjie
public static const HUKS_TAG_KEY_GENERATION_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 15
```

**Description:** Represents the tag for key generation type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_KEY_SECURE_SIGN_TYPE

```cangjie
public static const HUKS_TAG_KEY_SECURE_SIGN_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 308
```

**Description:** Specifies the signature type of the key when generating or importing it.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_TAG_KEY_SIZE

```cangjie
public static const HUKS_TAG_KEY_SIZE: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 3
```

**Description:** Represents the tag for key length.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_KEY_STORAGE_FLAG

```cangjie
public static const HUKS_TAG_KEY_STORAGE_FLAG: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 1002
```

**Description:** Represents the tag for key storage method.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_KEY_TYPE

```cangjie
public static const HUKS_TAG_KEY_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 7
```

**Description:** Represents the tag for key type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_KEY_WRAP_TYPE

```cangjie
public static const HUKS_TAG_KEY_WRAP_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 1004
```

**Description:** Reserved.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_NO_AUTH_REQUIRED

```cangjie
public static const HUKS_TAG_NO_AUTH_REQUIRED: UInt32 = HuksTagType.HUKS_TAG_TYPE_BOOL | 303
```

**Description:** Reserved.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_NONCE

```cangjie
public static const HUKS_TAG_NONCE: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 9
```

**Description:** Represents the NONCE field for key encryption/decryption.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_PADDING

```cangjie
public static const HUKS_TAG_PADDING: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 5
```

**Description:** Represents the tag for padding algorithm.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_PURPOSE

```cangjie
public static const HUKS_TAG_PURPOSE: UInt32 =  HuksTagType.HUKS_TAG_TYPE_UINT | 2
```

**Description:** Represents the tag for key purpose.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_RSA_PSS_SALT_LEN_TYPE

```cangjie
public static const HUKS_TAG_RSA_PSS_SALT_LEN_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 30
```

**Description:** Indicates the type of rsa_pss_salt_length.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_SALT

```cangjie
public static const HUKS_TAG_SALT: UInt32 = HuksTagType.HUKS_TAG_TYPE_BYTES | 12
```

**Description:** Represents the salt value during key derivation.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_UNWRAP_ALGORITHM_SUITE

```cangjie
public static const HUKS_TAG_UNWRAP_ALGORITHM_SUITE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 26
```

**Description:** Represents the suite for importing encrypted keys.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_USER_AUTH_TYPE

```cangjie
public static const HUKS_TAG_USER_AUTH_TYPE: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 304
```

**Description:** Indicates the user authentication type. Selected from [HuksUserAuthType](#class-huksuserauthtype), must be set together with secure access control type. Supports specifying two user authentication types simultaneously. For example: when the secure access control type is specified as HUKS_SECURE_ACCESS_INVALID_NEW_BIO_ENROLL, the key access authentication type can be one of the following three: HUKS_USER_AUTH_TYPE_FACE, HUKS_USER_AUTH_TYPE_FINGERPRINT, HUKS_USER_AUTH_TYPE_FACE MagIc_StrINg HUKS_USER_AUTH_TYPE_FINGERPRINT.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_TAG_USER_ID

```cangjie
public static const HUKS_TAG_USER_ID: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 302
```

**Description:** Indicates which userID the current key belongs to.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_AUTH_STORAGE_LEVEL

```cangjie
public static const HUKS_TAG_AUTH_STORAGE_LEVEL: UInt32 = HuksTagType.HUKS_TAG_TYPE_UINT | 316
```

**Description:** Key storage security level, which is a value of HuksAuthStorageLevel.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22## class HuksTagType

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

**Since:** 22

### static const HUKS_TAG_TYPE_BOOL

```cangjie
public static const HUKS_TAG_TYPE_BOOL: UInt32 = 4 << 28
```

**Description:** Indicates that the Tag's data type is boolean.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_TYPE_BYTES

```cangjie
public static const HUKS_TAG_TYPE_BYTES: UInt32 = 5 << 28
```

**Description:** Indicates that the Tag's data type is Uint8Array.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_TYPE_INT

```cangjie
public static const HUKS_TAG_TYPE_INT: UInt32 = 1 << 28
```

**Description:** Indicates that the Tag's data type is UInt32.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_TYPE_INVALID

```cangjie
public static const HUKS_TAG_TYPE_INVALID: UInt32 = 0 << 28
```

**Description:** Indicates an invalid Tag type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_TYPE_UINT

```cangjie
public static const HUKS_TAG_TYPE_UINT: UInt32 = 2 << 28
```

**Description:** Indicates that the Tag's data type is UInt32.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_TAG_TYPE_ULONG

```cangjie
public static const HUKS_TAG_TYPE_ULONG: UInt32 = 3 << 28
```

**Description:** Indicates that the Tag's data type is bigint.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

## class HuksUnwrapSuite

```cangjie
public class HuksUnwrapSuite {
    public static const HUKS_UNWRAP_SUITE_X25519_AES_256_GCM_NO_PADDING: UInt32 = 1
    public static const HUKS_UNWRAP_SUITE_ECDH_AES_256_GCM_NO_PADDING: UInt32 = 2
}
```

**Description:** Represents the algorithm suite for importing encrypted keys.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_UNWRAP_SUITE_ECDH_AES_256_GCM_NO_PADDING

```cangjie
public static const HUKS_UNWRAP_SUITE_ECDH_AES_256_GCM_NO_PADDING: UInt32 = 2
```

**Description:** When importing an encrypted key, uses AES-256 GCM encryption after ECDH key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### static const HUKS_UNWRAP_SUITE_X25519_AES_256_GCM_NO_PADDING

```cangjie
public static const HUKS_UNWRAP_SUITE_X25519_AES_256_GCM_NO_PADDING: UInt32 = 1
```

**Description:** When importing an encrypted key, uses AES-256 GCM encryption after X25519 key agreement.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

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

**Since:** 22

### static const HUKS_USER_AUTH_TYPE_FACE

```cangjie
public static const HUKS_USER_AUTH_TYPE_FACE: UInt32 = 1 << 1
```

**Description:** Indicates facial recognition as the user authentication type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_USER_AUTH_TYPE_FINGERPRINT

```cangjie
public static const HUKS_USER_AUTH_TYPE_FINGERPRINT: UInt32 = 1 << 0
```

**Description:** Indicates fingerprint recognition as the user authentication type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

### static const HUKS_USER_AUTH_TYPE_PIN

```cangjie
public static const HUKS_USER_AUTH_TYPE_PIN: UInt32 = 1 << 2
```

**Description:** Indicates PIN code as the user authentication type.

**Type:** UInt32

**System Capability:** SystemCapability.Security.Huks.Extension

**Since:** 22

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

**Description:** Used to represent the value of 'value' in HuksParam, supporting Bool, Int32, UInt32, UInt64, and Array\<UInt8> formats.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### BooleanValue(Bool)

```cangjie
BooleanValue(Bool)
```

**Description:** This field is used to pass a Bool-type value.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### BytesValue(Bytes)

```cangjie
BytesValue(Bytes)
```

**Description:** This field is used to pass a Bytes-type value.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### Int32Value(Int32)

```cangjie
Int32Value(Int32)
```

**Description:** This field is used to pass an Int32-type value.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### Uint32Value(UInt32)

```cangjie
Uint32Value(UInt32)
```

**Description:** This field is used to pass a UInt32-type value.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22

### Uint64Value(UInt64)

```cangjie
Uint64Value(UInt64)
```

**Description:** This field is used to pass a UInt64-type value.

**System Capability:** SystemCapability.Security.Huks.Core

**Since:** 22