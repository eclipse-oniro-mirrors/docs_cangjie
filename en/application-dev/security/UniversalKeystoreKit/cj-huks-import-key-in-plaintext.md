# Plaintext Key Import (Cangjie)

The following examples demonstrate importing AES256 and RSA2048 keys. For specific usage scenarios and supported algorithm specifications, refer to [Supported Algorithms for Key Import](./cj-huks-key-import-overview.md#supported-algorithms).

## Development Steps

1. Specify a key alias `keyAlias`.

   The maximum length of a key alias is 128 bytes.

2. Encapsulate the key property set and key material.

   - The key property set must be consistent with the properties specified during key generation and should include [HuksKeyAlg](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-hukskeyalg), [HuksKeySize](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-hukskeysize), and [HuksKeyPurpose](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-hukskeypurpose) attributes.
   - The key material must conform to the [HUKS Key Material Format](./cj-huks-concepts.md#key-material-format) and be assigned to the `inData` field of [HuksOptions](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksoptions) as an `Array<UInt8>`.

3. Call [importKeyItem](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-importkeyitemstring-huksoptions) with the key alias and key property set to import the key.

   For the meanings of `HuksParam` and `HuksOptions`, refer to: [HuksParam](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksparam) and [HuksOptions](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksoptions).

### Importing an AES256 Key

<!-- compile -->

```cangjie
/* The following demonstrates importing an AES256 key using Callback operations */
/* The following demonstrates generating a DH key as an example */
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.UniversalKeystoreKit.*

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

/* Key material */
let plainTextSize32: Array<UInt8> = [0xfb, 0x8b, 0x9f, 0x12, 0xa0, 0x83, 0x19, 0xbe, 0x6a, 0x6f, 0x63, 0x2a, 0x7c, 0x86,
    0xba, 0xca, 0x64, 0x0b, 0x88, 0x96, 0xe2, 0xfa, 0x77, 0xbc, 0x71, 0xe3, 0x0f, 0x0f, 0x9e, 0x3c, 0xe5, 0xf9]

/* 1. Define the key alias */
let keyAlias = 'AES256Alias_sample'

/* 2. Encapsulate the key property set and key material */
let properties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HuksTagAlgorithm,
        HuksKeyAlg.HUKS_ALG_AES
    ),
    HuksParam(
        HuksTag.HuksTagKeySize,
        HuksKeySize.HUKS_AES_KEY_SIZE_256
    ),
    HuksParam(
        HuksTag.HuksTagPurpose,
        HuksParamValue.Uint32Value(1 | 2)
    )
]
let options: HuksOptions = HuksOptions(
    properties: properties,
    inData: plainTextSize32
)

/* 3. Import the key in plaintext */
func importKeyFunc(): Unit {
    try {
        importKeyItem(keyAlias, options)
    } catch (e: Exception) {
        loggerInfo("callback: importKeyItem input arg invalid ${e}")
    }
}
```

### Importing an X25519 Public Key

<!-- compile -->

```cangjie
/* The following demonstrates generating a DH key as an example */
import kit.UniversalKeystoreKit.*

// X25519 public key data. Both the private and public keys in an X25519 key pair are 32 bytes (256 bits). For algorithm principles, refer to relevant cryptographic literature.
let x25519KeyPubMaterial: Array<UInt8> = [0x30, 0x2A, 0x30, 0x05, 0x06, 0x03, 0x2B, 0x65, 0x6E, 0x03, 0x21, 0x00, 0xD2,
    0x36, 0x9E, 0xCF, 0xF0, 0x61, 0x5B, 0x73, 0xCE, 0x4F, 0xF0, 0x40, 0x2B, 0x89, 0x18, 0x3E, 0x06, 0x33, 0x60, 0xC6]

/* 1. Define the key alias */
let keyAlias = 'X25519_Pub_import_sample'

/* 2. Encapsulate the key property set and key material */
let properties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksKeyAlg.HUKS_ALG_X25519
    ),
    HuksParam(
        HuksTag.HUKS_TAG_KEY_SIZE,
        HuksKeySize.HUKS_CURVE25519_KEY_SIZE_256
    ),
    HuksParam(
        // This tag indicates the purpose of the imported key and cannot be changed after import.
        HuksTag.HUKS_TAG_PURPOSE,
        HuksKeyPurpose.HUKS_KEY_PURPOSE_VERIFY
    ),
    HuksParam(
        // This tag indicates the type of key to import.
        HuksTag.HUKS_TAG_IMPORT_KEY_TYPE,
        // This value indicates importing a public key. Changing it to HUKS_KEY_TYPE_KEY_PAIR imports a key pair.
        HuksImportKeyType.HUKS_KEY_TYPE_PUBLIC_KEY
    )
]
let options: HuksOptions = HuksOptions(
    properties,
    x25519KeyPubMaterial
)

/* 3. Import the key in plaintext */
func importKeyFunc(): Unit {
    try {
        importKeyItem(keyAlias, options)
    } catch (e: Exception) {
        AppLog.error("callback: importKeyItem input arg invalid ${e}")
    }
}
```

## Debugging and Verification

Call [isKeyItemExist](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-iskeyitemexiststring-huksoptions) to verify if the key exists. If the key exists, the import was successful.

<!-- compile -->

```cangjie
import kit.UniversalKeystoreKit.*

let keyAlias = 'AES256Alias_sample'
let isKeyExist = false
let keyProperties: Array<HuksParam> = [
    HuksParam(
        HuksTag.HUKS_TAG_ALGORITHM,
        HuksKeyAlg.HUKS_ALG_AES
    )
]
let huksOptions: HuksOptions = HuksOptions(
    keyProperties, // Non-empty fill.
    None // Non-empty fill.
)

@Entry
@Component
class EntryView {
    @State
    var message: String = "Hello World"

    func build() {
        Row {
            Column {
                Text(this.message)
                    .fontSize(50)
                    .fontWeight(FontWeight.Bold)
                    .onClick {
                        evt => try {
                            isKeyItemExist(keyAlias, huksOptions)
                        } catch (e: Exception) {
                            AppLog.error(e)
                            throw e
                        }
                    }
            }.width(100.percent)
        }.height(100.percent)
    }
}
```