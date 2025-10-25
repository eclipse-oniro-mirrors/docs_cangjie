# Signature/Verification (Cangjie)

This guide provides four examples for developers to reference when implementing signature and verification development:

- [Signature/Verification (Cangjie)](#signatureverification-cangjie)
  - [Development Steps](#development-steps)
    - [Key Generation](#key-generation)
    - [Signature](#signature)
    - [Verification](#verification)
    - [Key Deletion](#key-deletion)
  - [Development Examples](#development-examples)
    - [ECC256/SHA256](#ecc256sha256)
    - [SM2/SM3](#sm2sm3)
    - [RSA/SHA256/PSS](#rsasha256pss)
    - [RSA/SHA256/PKCS1_V1_5](#rsasha256pkcs1_v1_5)

For specific scenario descriptions and supported algorithm specifications, please refer to [Supported Algorithms for Signature/Verification](./cj-huks-signing-signature-verification-overview.md#supported-algorithms).

## Development Steps

### Key Generation

1. Specify a key alias.

2. Initialize the key property set.

3. Call [generateKeyItem](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-generatekeyitemstring-huksoptions) to generate the key. For details, see [Key Generation](./cj-huks-key-generation-overview.md).

Alternatively, developers can reference [Key Import](./cj-huks-key-import-overview.md) to import existing keys.

### Signature

1. Obtain the key alias.

2. Specify the plaintext data to be signed.

3. Obtain the attribute parameter HuksOptions, which includes two fields: properties and inData. Pass the plaintext data to inData and the [algorithm parameter configuration](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksparam) to properties.

4. Call [initSession](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-initsessionstring-huksoptions) to initialize the key session and obtain the session handle.

5. Call [finishSession](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-finishsessionhukshandle-huksoptions) to end the key session and obtain the signature.

### Verification

1. Obtain the key alias.

2. Obtain the signature to be verified.

3. Obtain the attribute parameter HuksOptions, which includes two fields: properties and inData. Pass the signature to inData and the [algorithm parameter configuration](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksparam) to properties.

4. Call [initSession](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-initsessionstring-huksoptions) to initialize the key session and obtain the session handle.

5. Call [updateSession](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-updatesessionhukshandle-huksoptions) to update the key session.

6. Call [finishSession](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-finishsessionhukshandle-huksoptions) to end the key session and verify the signature.

### Key Deletion

When a key is no longer needed, call [deleteKeyItem](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-deletekeyitemstring-huksoptions) to delete it. For details, see [Key Deletion](./cj-huks-delete-key.md).

## Development Examples

### ECC256/SHA256

<!--compile-->
```cangjie
/*
 * Key algorithm: ECC256; Digest algorithm: SHA256
 */
import kit.UniversalKeystoreKit.*

let keyAlias = 'test_eccKeyAlias'
var handle: ?HuksHandle = None
let plaintext = '123456'
var signature: ?Array<UInt8> = None

func StringToUint8Array(str: String) {
    return str.toArray()
}

func Uint8ArrayToString(fileData: Array<UInt8>) {
    return String.fromUtf8(fileData)
}

func GetEccGenerateProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksKeyAlg.HUKS_ALG_ECC
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksKeySize.HUKS_AES_KEY_SIZE_256
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_SIGN | HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksKeyDigest.HUKS_DIGEST_SHA256
        )
    ]
    return properties
}

func GetEccSignProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksKeyAlg.HUKS_ALG_ECC
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksKeySize.HUKS_AES_KEY_SIZE_256
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_SIGN
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksKeyDigest.HUKS_DIGEST_SHA256
        )
    ]
    return properties
}

func GetEccVerifyProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksKeyAlg.HUKS_ALG_ECC
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksKeySize.HUKS_AES_KEY_SIZE_256
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksKeyDigest.HUKS_DIGEST_SHA256
        )
    ]
    return properties
}

func GenerateEccKey(keyAlias: String) {
    let genProperties = GetEccGenerateProperties()
    let options: HuksOptions = HuksOptions(genProperties, None)
    generateKeyItem(keyAlias, options)
}

func Sign(keyAlias: String, plaintext: String) {
    let signProperties = GetEccSignProperties()
    let options: HuksOptions = HuksOptions(
        signProperties,
        StringToUint8Array(plaintext)
    )
    handle = initSession(keyAlias, options).handle
    signature = finishSession(handle.getOrThrow(), options)
}

func Verify(keyAlias: String, plaintext: String, signature: Array<UInt8>) {
    let verifyProperties = GetEccVerifyProperties()
    var options: HuksOptions = HuksOptions(
        verifyProperties,
        StringToUint8Array(plaintext)
    )
    handle = initSession(keyAlias, options).handle
    updateSession(handle.getOrThrow(), options)
    options.inData = signature
    finishSession(handle.getOrThrow(), options)
}

func DeleteEccKey(keyAlias: String) {
    let emptyOptions: HuksOptions = HuksOptions.NONE
    deleteKeyItem(keyAlias, emptyOptions)
}

func testSignVerify() {
    GenerateEccKey(keyAlias)
    Sign(keyAlias, plaintext)
    Verify(keyAlias, plaintext, signature.getOrThrow())
    DeleteEccKey(keyAlias)
}
```

### SM2/SM3

```cangjie
/*
 * Key algorithm: SM2; Digest algorithm: SM3
 */
import kit.UniversalKeystoreKit.*

let keyAlias = 'test_sm2KeyAlias'
var handle: ?HuksHandle = None
let plaintext = '123456'
var signature: ?Array<UInt8> = None

func StringToUint8Array(str: String) {
    return str.toArray()
}

func Uint8ArrayToString(fileData: Array<UInt8>) {
    return String.fromUtf8(fileData)
}

func GetSm2GenerateProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksKeyAlg.HUKS_ALG_SM2
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksKeySize.HUKS_AES_KEY_SIZE_256
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_SIGN | HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksKeyDigest.HUKS_DIGEST_SM3
        )
    ]
    return properties
}

func GetSm2SignProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksKeyAlg.HUKS_ALG_SM2
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksKeySize.HUKS_AES_KEY_SIZE_256
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_SIGN
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksKeyDigest.HUKS_DIGEST_SM3
        )
    ]
    return properties
}

func GetSm2VerifyProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksKeyAlg.HUKS_ALG_SM2
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksKeySize.HUKS_AES_KEY_SIZE_256
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksKeyDigest.HUKS_DIGEST_SM3
        )
    ]
    return properties
}

func GenerateSm2Key(keyAlias: String) {
    let genProperties = GetSm2GenerateProperties()
    let options: HuksOptions = HuksOptions(genProperties, None)
    generateKeyItem(keyAlias, options)
}

func Sign(keyAlias: String, plaintext: String) {
    let signProperties = GetSm2SignProperties()
    let options: HuksOptions = HuksOptions(
        signProperties,
        StringToUint8Array(plaintext)
    )
    handle = initSession(keyAlias, options).handle
    signature = finishSession(handle.getOrThrow(), options)
}

func Verify(keyAlias: String, plaintext: String, signature: Array<UInt8>) {
    let verifyProperties = GetSm2VerifyProperties()
    var options: HuksOptions = HuksOptions(
        verifyProperties,
        StringToUint8Array(plaintext)
    )
    handle = initSession(keyAlias, options).handle
    updateSession(handle.getOrThrow(), options)
    options.inData = signature
    finishSession(handle.getOrThrow(), options)
}

func DeleteSm2Key(keyAlias: String) {
    let emptyOptions: HuksOptions = HuksOptions.NONE
    deleteKeyItem(keyAlias, emptyOptions)
}

func testSignVerify() {
    GenerateSm2Key(keyAlias)
    Sign(keyAlias, plaintext)
    Verify(keyAlias, plaintext, signature.getOrThrow())
    DeleteSm2Key(keyAlias)
}
```

### RSA/SHA256/PSS

<!--compile-->
```cangjie
/*
 * Key algorithm: RSA, Digest algorithm: SHA256, Padding mode: PSS
 */
import kit.UniversalKeystoreKit.*

let keyAlias = 'test_rsaKeyAlias'
var handle: ?HuksHandle = None
let plaintext = '123456'
var signature: ?Array<UInt8> = None

func StringToUint8Array(str: String) {
    return str.toArray()
}

func Uint8ArrayToString(fileData: Array<UInt8>) {
    return String.fromUtf8(fileData)
}

func GetRsaGenerateProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksKeyAlg.HUKS_ALG_RSA
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksKeySize.HUKS_RSA_KEY_SIZE_2048
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_SIGN | HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PADDING,
            HuksKeyPadding.HUKS_PADDING_PSS
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksKeyDigest.HUKS_DIGEST_SHA256
        )
    ]
    return properties
}

func GetRsaSignProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksKeyAlg.HUKS_ALG_RSA
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PADDING,
            HuksKeyPadding.HUKS_PADDING_PSS
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksKeyDigest.HUKS_DIGEST_SHA256
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_SIGN
        )
    ]
    return properties
}

func GetRsaVerifyProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksKeyAlg.HUKS_ALG_RSA
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PADDING,
            HuksKeyPadding.HUKS_PADDING_PSS
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksKeyDigest.HUKS_DIGEST_SHA256
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY
        )
    ]
    return properties
}

func GenerateRsaKey(keyAlias: String) {
    let genProperties = GetRsaGenerateProperties()
    let options: HuksOptions = HuksOptions(genProperties, None)
    generateKeyItem(keyAlias, options)
}

func Sign(keyAlias: String, plaintext: String) {
    let signProperties = GetRsaSignProperties()
    let options: HuksOptions = HuksOptions(
        signProperties,
        StringToUint8Array(plaintext)
    )
    handle = initSession(keyAlias, options).handle

    if (let Some(handle) <- handle) {
        signature = finishSession(handle, options)
    }
}

func Verify(keyAlias: String, plaintext: String, signature: Array<UInt8>) {
    let verifyProperties = GetRsaVerifyProperties()
    var options: HuksOptions = HuksOptions(
        verifyProperties,
        StringToUint8Array(plaintext)
    )
    handle = initSession(keyAlias, options).handle

    if (let Some(handle) <- handle) {
        updateSession(handle, options)

        options.inData = signature
        finishSession(handle, options)
    }
}

func DeleteRsaKey(keyAlias: String) {
    let emptyOptions: HuksOptions = HuksOptions.NONE
    deleteKeyItem(keyAlias, emptyOptions)
}

func testSignVerify() {
    GenerateRsaKey(keyAlias)
    Sign(keyAlias, plaintext)
    Verify(keyAlias, plaintext, signature.getOrThrow())
    DeleteRsaKey(keyAlias)
}
```

### RSA/SHA256/PKCS1_V1_5

<!--compile-->
```cangjie
/*
 * Key algorithm: RSA, Digest algorithm: SHA256, Padding mode: PKCS1_V1_5
 */
import kit.UniversalKeystoreKit.*

let keyAlias = 'test_rsaKeyAlias'
var handle: ?HuksHandle = None
let plaintext = '123456'
var signature: ?Array<UInt8> = None

func StringToUint8Array(str: String) {
    return str.toArray()
}

func Uint8ArrayToString(fileData: Array<UInt8>) {
    return String.fromUtf8(fileData)
}

func GetRsaGenerateProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(HUKS_TAG_ALGORITHM, HuksKeyAlg.HUKS_ALG_RSA),
        HuksParam(HUKS_TAG_KEY_SIZE, HuksKeySize.HUKS_RSA_KEY_SIZE_2048),
        HuksParam(
            HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_SIGN | HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY
        ),
        HuksParam(HUKS_TAG_PADDING, HuksKeyPadding.HUKS_PADDING_PKCS1_V1_5),
        HuksParam(HUKS_TAG_DIGEST, HuksKeyDigest.HUKS_DIGEST_SHA256)
    ]
    return properties
}

func GetRsaSignProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HUKS_TAG_ALGORITHM,
            HuksKeyAlg.HUKS_ALG_RSA
        ),
        HuksParam(
            HUKS_TAG_KEY_SIZE,
            HuksKeySize.HUKS_RSA_KEY_SIZE_2048
        ),
        HuksParam(
            HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_SIGN
        ),
        HuksParam(
            HUKS_TAG_PADDING,
            HuksKeyPadding.HUKS_PADDING_PKCS1_V1_5
        ),
        HuksParam(
            HUKS_TAG_DIGEST,
            HuksKeyDigest.HUKS_DIGEST_SHA256
        )
    ]
    return properties
}

func GetRsaVerifyProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HUKS_TAG_ALGORITHM,
            HuksKeyAlg.HUKS_ALG_RSA
        ),
        HuksParam(
            HUKS_TAG_KEY_SIZE,
            HuksKeySize.HUKS_RSA_KEY_SIZE_2048
        ),
        HuksParam(
            HUKS_TAG_PURPOSE,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY
        ),
        HuksParam(
            HUKS_TAG_PADDING,
            HuksKeyPadding.HUKS_PADDING_PKCS1_V1_5
        ),
        HuksParam(
            HUKS_TAG_DIGEST,
            HuksKeyDigest.HUKS_DIGEST_SHA256
        )
    ]
    return properties
}

func GenerateRsaKey(keyAlias: String) {
    let genProperties = GetRsaGenerateProperties()
    let options: HuksOptions = HuksOptions(genProperties, None)
    generateKeyItem(keyAlias, options)
}

func Sign(keyAlias: String, plaintext: String) {
    let signProperties = GetRsaSignProperties()
    let options: HuksOptions = HuksOptions(
        signProperties,
        StringToUint8Array(plaintext)
    )
    handle = initSession(keyAlias, options).handle
    signature = finishSession(handle.getOrThrow(), options)
}

func Verify(keyAlias: String, plaintext: String, signature: Array<UInt8>) {
    let verifyProperties = GetRsaVerifyProperties()
    var options: HuksOptions = HuksOptions(
        verifyProperties,
        StringToUint8Array(plaintext)
    )
    handle = initSession(keyAlias, options).handle
    updateSession(handle.getOrThrow(), options)
    options.inData = signature
    finishSession(handle.getOrThrow(), options)
}

func DeleteRsaKey(keyAlias: String) {
    let emptyOptions: HuksOptions = HuksOptions.NONE
    deleteKeyItem(keyAlias, emptyOptions)
}

func testSignVerify() {
    GenerateRsaKey(keyAlias)
    Sign(keyAlias, plaintext)
    Verify(keyAlias, plaintext, signature.getOrThrow())
    DeleteRsaKey(keyAlias)
}
```