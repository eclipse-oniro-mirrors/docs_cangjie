# Non-Anonymous Key Attestation (Cangjie)

Before using this feature, you need to apply for the permission: [ohos.permission.ATTEST_KEY](../AccessToken/cj-permissions-for-system-apps.md#ohospermissionattest_key). Developers should refer to the specific operation path [Permission Application](../AccessToken/cj-determine-application-mode.md) based on the application's APL level.

## Development Steps

1. Determine the key alias `keyAlias`. The maximum length of the key alias is 128 bytes.

2. Initialize the parameter set. The `properties` field in [HuksOptions](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksoptions) must include the [HUKS_TAG_ATTESTATION_CHALLENGE](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#enum-hukstag) attribute. Optional parameters include [HUKS_TAG_ATTESTATION_ID_VERSION_INFO](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#enum-hukstag) and [HUKS_TAG_ATTESTATION_ID_ALIAS](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#enum-hukstag).

3. Generate an asymmetric key. For details, refer to [Key Generation](./cj-huks-key-generation-overview.md).

4. Pass the key alias and parameter set as parameters to the [huks.attestKeyItem](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-attestkeyitemstring-huksoptions) method to attest the key.

<!--compile-->
```cangjie
import kit.UniversalKeystoreKit.*

/* 1. Determine key alias */
let keyAliasString = "key anon attest"
let aliasString = keyAliasString
let aliasUint8 = StringToUint8Array(keyAliasString)
let securityLevel = StringToUint8Array('sec_level')
let challenge = StringToUint8Array('challenge_data')
let versionInfo = StringToUint8Array('version_info')
var attestCertChain: ?Array<String> = None

class ThrowObject {
    var isThrow: Bool = false

    init(isThrow: Bool) {
        this.isThrow = isThrow
    }
}

/* Encapsulate key parameters for generation */
let genKeyProperties: Array<HuksParam> = [
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
        HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksKeyDigest.HUKS_DIGEST_SHA256
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PADDING,
        HuksKeyPadding.HUKS_PADDING_PSS
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_GENERATE_TYPE,
        HuksKeyGenerateType.HUKS_KEY_GENERATE_TYPE_DEFAULT
    ),
    HuksParam(
        HuksTag.HUKS_TAG_BLOCK_MODE,
        HuksCipherMode.HUKS_MODE_ECB
    )
]
let genOptions: HuksOptions = HuksOptions(genKeyProperties, Option<Array<UInt8>>.None)

/* 2. Encapsulate key attestation parameters */
let anonAttestKeyProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ATTESTATION_ID_SEC_LEVEL_INFO,
        bytes(securityLevel)
    ),
    HuksParam(
        HuksTag.HUKS_TAG_ATTESTATION_CHALLENGE,
        bytes(challenge)
    ),
    HuksParam(
        HuksTag.HUKS_TAG_ATTESTATION_ID_VERSION_INFO,
        bytes(versionInfo)
    ),
    HuksParam(
        HuksTag.HUKS_TAG_ATTESTATION_ID_ALIAS,
        bytes(aliasUint8)
    )
]
let huksOptions: HuksOptions = HuksOptions(anonAttestKeyProperties, Option<Array<UInt8>>.None)

func StringToUint8Array(str: String) {
    return str.toArray()
}

func generateKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
    try {
        generateKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

/* 3. Generate key */
func publicGenKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
    AppLog.info("enter generateKeyItem")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        generateKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        AppLog.error("generateKeyItem input arg invalid, ${e}")
    }
}

/* 4. Attest key */
func attestKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
    return try {
        attestKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicAttestKey(keyAlias: String, huksOptions: HuksOptions) {
    AppLog.info("enter attestKeyItem")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        attestCertChain = attestKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        AppLog.error("attestKeyItem input arg invalid, ${e}")
    }
}

func attestKeyTest() {
    publicGenKeyFunc(aliasString, genOptions)
    publicAttestKey(aliasString, huksOptions)
    AppLog.info('anon attest certChain data: ' + attestCertChain.getOrThrow().toString())
}
```