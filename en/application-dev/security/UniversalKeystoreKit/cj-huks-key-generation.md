# Generating Keys (Cangjie)

Taking the generation of DH keys as an example, this section demonstrates how to generate random keys. For specific usage scenarios and supported algorithm specifications, please refer to [Supported Algorithms for Key Generation](./cj-huks-key-generation-overview.md#supported-algorithms).

> **Note:**
>
> Key aliases must not contain sensitive information such as personal data.

## Development Procedure

1. Specify the key alias `keyAlias` to be generated.

    - The maximum length of a key alias is 128 bytes. It is recommended to avoid including sensitive terms such as personal information.
    - For keys generated across different services, HUKS will isolate storage paths based on service identity information, preventing conflicts due to identical key names in different services.

2. Initialize the key property set. Encapsulate key properties via [HuksParam](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksparam), combine them into an Array to form the key property set, and assign it to the `properties` field in [HuksOptions](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-huksoptions).

    The key property set must include [HuksKeyAlg](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-hukskeyalg), [HuksKeySize](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-hukskeysize), and [HuksKeyPurpose](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#class-hukskeypurpose) properties, i.e., mandatory tags: `HUKS_TAG_ALGORITHM`, `HUKS_TAG_PURPOSE`, and `HUKS_TAG_KEY_SIZE`. Note: A key can only have one type of `PURPOSE`, and the purpose specified during key generation must match the usage method; otherwise, exceptions may occur. For details, refer to [Key Purpose](./cj-huks-key-generation-overview.md#key-purpose).

3. Call [generateKeyItem](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-generatekeyitemstring-huksoptions), passing the key alias and key property set to generate the key.

> **Note:**
>
> If a service calls HUKS to generate a key again using the same alias, HUKS will generate a new key and directly overwrite the historical key file.

## Example

<!--compile-->
```cangjie
/* Example: Generating a DH Key */
import kit.UniversalKeystoreKit.*

/* 1. Define the key alias */
let keyAlias = 'dh_key'
/* 2. Initialize the key property set */
let properties1: Array<HuksParam> = [
  HuksParam(
    HuksTag.HUKS_TAG_ALGORITHM,
    HuksKeyAlg.HUKS_ALG_DH
  ),
  HuksParam(
    HuksTag.HUKS_TAG_PURPOSE,
    HuksKeyPurpose.HUKS_KEY_PURPOSE_AGREE
  ),
  HuksParam(
    HuksTag.HUKS_TAG_KEY_SIZE,
    HuksKeySize.HUKS_DH_KEY_SIZE_2048
  )
]
let huksOptions: HuksOptions = HuksOptions(
  properties1,
  None
)

/* 3. Generate the key */
func publicGenKeyFunc(keyAlias: String, huksOptions: HuksOptions) {
  AppLog.info("enter generateKeyItem")
  try {
    generateKeyItem(keyAlias, huksOptions)
  } catch (e: Exception) {
    AppLog.error("generateKeyItem input arg invalid, ${e}")
  }
}

func TestGenKey() {
  publicGenKeyFunc(keyAlias, huksOptions)
}
```