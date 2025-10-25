# Key Export (Cangjie)

Used when a business needs to obtain the public key of an asymmetrically stored persistent key. Currently supports public key export for ECC/RSA/ED25519/X25519/SM2.

> **Note:**
>
> Lightweight devices only support RSA public key export.

## Development Steps

1. Specify the key alias `keyAlias`, with a maximum length of 128 bytes.

2. Call the interface [`exportKeyItem`](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-exportkeyitemstring-huksoptions), passing the parameters `keyAlias` and `options`. `options` is a reserved parameter and can currently be left empty.

3. The return value is of type `Bytes`, encapsulated in the standard DER format of X.509 specification. For details, refer to [Public Key Material Format](./cj-huks-concepts.md#public-key-material-format).

## Example

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

/* 1. Set key alias */
let keyAlias = "keyAlias"

/* 2. Pass empty options object */
let emptyOptions: HuksOptions = HuksOptions(properties: [], inData: Bytes())

try {
    /* 3. Export public key */
    let b = exportKeyItem(keyAlias, emptyOptions)
    loggerInfo("exportKeyItem success")
} catch (e: Exception) {
    loggerInfo("exportKeyItem input arg invalid")
}

```