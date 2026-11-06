# Non-Anonymous Key Attestation (Cangjie)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Before using this feature, you need to apply for the permission: [ohos.permission.ATTEST_KEY](../AccessToken/cj-permissions-for-system-apps.md#ohospermissionattest_key). Developers should refer to the specific operation path [Permission Application](../AccessToken/cj-determine-application-mode.md) based on the application's APL level.

## Development Steps

1. Determine the key alias `keyAlias`. The maximum length of the key alias is 128 bytes.

2. Initialize the parameter set. The `properties` field in [HuksOptions](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksoptions) must include the [HUKS_TAG_ATTESTATION_CHALLENGE](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#enum-hukstag) attribute. Optional parameters may include [HUKS_TAG_ATTESTATION_ID_VERSION_INFO](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#enum-hukstag) and [HUKS_TAG_ATTESTATION_ID_ALIAS](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#enum-hukstag) attributes.

3. Generate an asymmetric key. For details, refer to [Key Generation](./cj-huks-key-generation-overview.md).

4. Pass the key alias and parameter set as arguments to the [huks.attestKeyItem](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-attestkeyitemstring-huksoptions) method to attest the key.

<!-- compile -->

```cangjie
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.UniversalKeystoreKit.*

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

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

/* Encapsulate key generation parameter set */
let genKeyProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_RSA)
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_SIZE,
        HuksParamValue.Uint32Value(HuksKeySize.HUKS_RSA_KEY_SIZE_2048)
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PURPOSE,
        HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY)
    ),
    HuksParam(
        HuksTag.HUKS_TAG_DIGEST,
        HuksParamValue.Uint32Value(HuksKeyDigest.HUKS_DIGEST_SHA256)
    ),
    HuksParam(
        HuksTag.HUKS_TAG_PADDING,
        HuksParamValue.Uint32Value(HuksKeyPadding.HUKS_PADDING_PSS)
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_GENERATION_TYPE,
        HuksParamValue.Uint32Value(HuksKeyGenerationType.HUKS_KEY_GENERATE_TYPE_DEFAULT)
    ),
    HuksParam(
        HuksTag.HUKS_TAG_BLOCK_MODE,
        HuksParamValue.Uint32Value(HuksCipherMode.HUKS_MODE_ECB)
    )
]
let genOptions: HuksOptions = HuksOptions(properties: genKeyProperties, inData: Bytes())

/* 2. Encapsulate key attestation parameter set */
let anonAttestKeyProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ATTESTATION_CHALLENGE,
        HuksParamValue.BytesValue(challenge.toArray())
    )
]
let huksOptions: HuksOptions = HuksOptions(properties: anonAttestKeyProperties, inData: Bytes())

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
    loggerInfo("enter generateKeyItem")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        generateKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("generateKeyItem input arg invalid, ${e}")
    }
}

/* 4. Attest key */
func attestKeyItemext(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject): Array<String> {
    return try {
        anonAttestKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicAttestKey(keyAlias: String, huksOptions: HuksOptions) {
    loggerInfo("enter attestKeyItem")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        attestCertChain = attestKeyItemext(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("attestKeyItem input arg invalid, ${e}")
    }
}

func attestKeyTest() {
    publicGenKeyFunc(aliasString, genOptions)
    publicAttestKey(aliasString, huksOptions)
    loggerInfo('anon attest certChain data: ' + attestCertChain.getOrThrow().toString())
}
```