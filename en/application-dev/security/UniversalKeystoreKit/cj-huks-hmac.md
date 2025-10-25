# HMAC (Cangjie)

HMAC stands for Hash-based Message Authentication Code, which is a key-dependent cryptographic hash function. For specific usage scenarios and supported algorithm specifications, please refer to [HMAC Introduction and Algorithm Specifications](./cj-huks-hmac-overview.md).

## Development Steps

### Generate Key

1. Specify a key alias.

2. Initialize the key property set.

3. Call [generateKeyItem](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-generatekeyitemstring-huksoptions) to generate the key. For HMAC-supported specifications, see [Key Generation](./cj-huks-key-generation-overview.md#supported-algorithms).

Alternatively, developers can refer to the specifications in [Key Import](./cj-huks-key-import-overview.md#supported-algorithms) to import an existing key.

### Perform HMAC

1. Obtain the key alias.

2. Get the data to be processed.

3. Call [initSession](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-initsessionstring-huksoptions) to initialize the key session and obtain the session handle.

4. Call [finishSession](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-finishsessionhukshandleid-huksoptions-bytes) to complete the key session and obtain the HMAC result.

## Example

<!-- compile -->

```cangjie
/*
 * The following demonstrates the usage of HMAC key operations
 */
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.UniversalKeystoreKit.*

let HmacKeyAlias = 'test_HMAC' // Key alias, user-defined for key generation
var handle: ?HuksHandleId = None
let plainText = '123456' // Data to be processed
var hashData: ?Array<UInt8> = None // Data after HMAC operation

func StringToUint8Array(str: String) {
    return str.toArray()
}

func Uint8ArrayToString(fileData: Array<UInt8>) {
    return String.fromUtf8(fileData)
}

func GetHMACProperties() {
    let properties: Array<HuksParam> = [
        HuksParam(
            HuksTag.HuksTagAlgorithm,
            HuksKeyAlg.HUKS_ALG_HMAC
        ),
        HuksParam(
            HuksTag.HuksTagKeySize,
            HuksKeySize.HUKS_KEY_SIZE_256
        ),
        HuksParam(
            HuksTag.HuksTagPurpose,
            HuksKeyPurpose.HUKS_KEY_PURPOSE_MAC
        ),
        HuksParam(
            HuksTag.HuksTagDigest,
            HuksKeyDigest.HUKS_DIGEST_SHA384
        )
    ]
    return properties
}

/*
 * Simulate key generation scenario
 */
func GenerateHMACKey() {
    // Get algorithm parameter configuration for key generation
    let genProperties = GetHMACProperties()
    let options: HuksOptions = HuksOptions(properties: genProperties, inData: Bytes())
    // Call generateKeyItem to generate the key. HmacKeyAlias is the key alias specified during key generation.
    generateKeyItem(HmacKeyAlias, options)
}

/*
 * Simulate HMAC calculation scenario
 */
func HMACData() {
    // Get HMAC algorithm parameter configuration
    let hmacProperties = GetHMACProperties()
    let options: HuksOptions = HuksOptions(
        properties: hmacProperties,
        inData: StringToUint8Array(plainText)
    )
    // Call initSession to obtain the handle. HmacKeyAlias is the key alias specified during key generation.
    handle = initSession(HmacKeyAlias, options)
    // Call finishSession to obtain the HMAC result
    hashData = finishSession(handle.getOrThrow(), options)
}
```