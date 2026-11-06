# HMAC (Cangjie)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

HMAC stands for Hash-based Message Authentication Code with keyed-hashing. For specific usage scenarios and supported algorithm specifications, please refer to [HMAC Introduction and Algorithm Specifications](./cj-huks-hmac-overview.md).

## Development Procedure

### Generate Key

1. Specify a key alias.

2. Initialize the key property set.

3. Call [generateKeyItem](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-generatekeyitemstring-huksoptions) to generate the key. For HMAC-supported specifications, see [Key Generation](./cj-huks-key-generation-overview.md#supported-algorithms).

Alternatively, developers can refer to the specifications in [Key Import](./cj-huks-key-import-overview.md#supported-algorithms) to import an existing key.

### Perform HMAC

1. Obtain the key alias.

2. Obtain the data to be processed.

3. Call [initSession](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-initsessionstring-huksoptions) to initialize the key session and obtain the session handle.

4. Call [finishSession](../../reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-finishsessionhukshandleid-huksoptions-bytes) to complete the key session and obtain the HMAC result.

## Example

<!-- compile -->

```cangjie
/*
 * The following demonstrates HMAC key operations
 */
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.UniversalKeystoreKit.*

let hmacKeyAlias = 'test_HMAC' // Key alias, user-defined for key generation
var handle: ?HuksHandleId = None
let plainText = '123456' // Data to be processed
var hashData: ?Array<UInt8> = None // HMAC-processed data

func stringToUint8Array(str: String) {
    return str.toArray()
}

func uint8ArrayToString(fileData: Array<UInt8>) {
    return String.fromUtf8(fileData)
}

func getHmacProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HUKS_TAG_ALGORITHM,
            HuksParamValue.Uint32Value(HuksKeyAlg.HUKS_ALG_HMAC)
        ),
        HuksParam(
            HuksTag.HUKS_TAG_KEY_SIZE,
            HuksParamValue.Uint32Value(HuksKeySize.HUKS_AES_KEY_SIZE_256)
        ),
        HuksParam(
            HuksTag.HUKS_TAG_PURPOSE,
            HuksParamValue.Uint32Value(HuksKeyPurpose.HUKS_KEY_PURPOSE_MAC)
        ),
        HuksParam(
            HuksTag.HUKS_TAG_DIGEST,
            HuksParamValue.Uint32Value(HuksKeyDigest.HUKS_DIGEST_SHA384)
        )
    ]
    return properties
}

/*
 * Simulate key generation scenario
 */
func generateHmacKey() {
    // Obtain key generation algorithm parameter configuration
    let genProperties = getHmacProperties()
    let options: HuksOptions = HuksOptions(properties: genProperties, inData: Bytes())
    // Call generateKeyItem to generate the key. hmacKeyAlias is the key alias specified during key generation
    generateKeyItem(hmacKeyAlias, options)
}

/*
 * Simulate HMAC computation scenario
 */
func hmacData() {
    // Obtain HMAC algorithm parameter configuration
    let hmacProperties = getHmacProperties()
    let options: HuksOptions = HuksOptions(
        properties: hmacProperties,
        inData: stringToUint8Array(plainText)
    )
    // Call initSession to obtain the handle. hmacKeyAlias is the key alias specified during key generation
    handle = initSession(hmacKeyAlias, options).handle
    // Call finishSession to obtain the HMAC result
    hashData = finishSession(handle.getOrThrow(), options)
}
```