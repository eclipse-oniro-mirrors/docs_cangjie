# Anonymous Key Attestation (Cangjie)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Ensure network connectivity is available when using this feature.

## Development Procedure

1. Determine the key alias `keyAlias`. The maximum length of the key alias is 128 bytes.

2. Initialize the parameter set.

   The properties field in [HuksOptions](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksoptions) must include the [HUKS_TAG_ATTESTATION_CHALLENGE](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#enum-hukstag) attribute. Optional parameters may include [HUKS_TAG_ATTESTATION_ID_VERSION_INFO](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#enum-hukstag) and [HUKS_TAG_ATTESTATION_ID_ALIAS](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#enum-hukstag) attributes.

3. Generate an asymmetric key. For details, refer to [Key Generation](./cj-huks-key-generation-overview.md).

4. Pass the key alias and parameter set as arguments to the [anonAttestKeyItem](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-anonattestkeyitemstring-huksoptions) method to attest the key.

## Complete Example

<!-- compile -->

```cangjie
/*
 * The following demonstrates interface operations for anonAttestKey verification
 */
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
let aliasUint8 = stringToUint8Array(keyAliasString)
let securityLevel = stringToUint8Array('sec_level')
let challenge = stringToUint8Array('challenge_data')
let versionInfo = stringToUint8Array('version_info')
var anonAttestCertChain: ?Array<String> = None

class ThrowObject {
    var isThrow: Bool = false

    init(isThrow: Bool) {
        this.isThrow = isThrow
    }
}

/* Encapsulate key parameters during generation */
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
let genOptions: HuksOptions = HuksOptions(properties: genKeyProperties, inData: Option<Array<UInt8>>.None.getOrThrow())

/* 2. Encapsulate key attestation parameters */
let anonAttestKeyProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ATTESTATION_CHALLENGE,
        HuksParamValue.BytesValue(challenge.toArray())
    )
]
let huksOptions: HuksOptions = HuksOptions(properties: anonAttestKeyProperties, inData: Option<Array<UInt8>>.None.getOrThrow())

func stringToUint8Array(str: String) {
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
func anonAttestKeyItem(keyAlias: String, huksOptions: HuksOptions, throwObject: ThrowObject) {
    return try {
        anonAttestKeyItem(keyAlias, huksOptions)
    } catch (e: Exception) {
        throwObject.isThrow = true
        throw e
    }
}

func publicAnonAttestKey(keyAlias: String, huksOptions: HuksOptions) {
    loggerInfo("enter anonAttestKeyItem")
    let throwObject: ThrowObject = ThrowObject(false)
    try {
        anonAttestCertChain = anonAttestKeyItem(keyAlias, huksOptions, throwObject)
    } catch (e: Exception) {
        loggerInfo("anonAttestKeyItem input arg invalid, ${e}")
    }
}

func anonAttestKeyTest() {
    publicGenKeyFunc(aliasString, genOptions)
    publicAnonAttestKey(aliasString, huksOptions)
    loggerInfo('anon attest certChain data: ' + anonAttestCertChain.getOrThrow().toString())
}
```