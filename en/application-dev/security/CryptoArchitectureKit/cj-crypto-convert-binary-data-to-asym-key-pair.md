# Converting Binary Data to an Asymmetric Key Pair

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Taking RSA, ECC, and SM2 as examples, an asymmetric key pair (KeyPair) is generated based on the specified asymmetric key binary data—that is, converting external or stored binary data into a key object of the algorithm library. This object can be used for subsequent operations such as encryption and decryption.

> **Note:**
>
> For the convertKey operation on asymmetric keys:
>
> - Public keys must comply with ASN.1 syntax, X.509 specifications, and DER encoding format.
>
> - Private keys must comply with ASN.1 syntax, PKCS\#8 specifications, and DER encoding format.

## Converting Binary Data to an RSA Key Pair

For the corresponding algorithm specifications, see [Asymmetric Key Generation and Conversion Specifications: RSA](./cj-crypto-asym-key-generation-conversion-spec.md#rsa).

1. Obtain the RSA public key or private key binary data and encapsulate it into a [DataBlob](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#class-datablob) object.

   The public key and private key can be passed in separately. This example passes in the public key.

2. Call [createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring), specifying the string parameter 'RSA1024', to create an asymmetric key generator (AsyKeyGenerator) with RSA key type RSA1024 and 2 primes.

   When generating RSA asymmetric keys, the default number of primes is 2, so the parameter PRIMES_2 is omitted here.

3. Call [convertKey](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-convertkeyasynccallbackkeypairoptiondatabloboptiondatablob), passing in the binary key data to generate an asymmetric key object (KeyPair). This converts external or stored binary data into a key object of the algorithm library, which can be used for subsequent operations such as encryption and decryption.

The following example uses converting an RSA public key:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.AsyncCallback
import kit.PerformanceAnalysisKit.Hilog

func testConvertRSAKey() {
    let asyKeyGenerator = createAsyKeyGenerator("RSA1024")
    let pkVal: Array<UInt8> = [48, 129, 159, 48, 13, 6, 9, 42, 134, 72, 134, 247, 13, 1, 1, 1, 5, 0, 3, 129, 141, 0, 48, 129, 137,
        2, 129, 129, 0, 174, 203, 113, 83, 113, 3, 143, 213, 194, 79, 91, 9, 51, 142, 87, 45, 97, 65, 136, 24, 166, 35, 5,
        179, 42, 47, 212, 79, 111, 74, 134, 120, 73, 67, 21, 19, 235, 80, 46, 152, 209, 133, 232, 87, 192, 140, 18, 206,
        27, 106, 106, 169, 106, 46, 135, 111, 118, 32, 129, 27, 89, 255, 183, 116, 247, 38, 12, 7, 238, 77, 151, 167, 6,
        102, 153, 126, 66, 28, 253, 253, 216, 64, 20, 138, 117, 72, 15, 216, 178, 37, 208, 179, 63, 204, 39, 94, 244, 170,
        48, 190, 21, 11, 73, 169, 156, 104, 193, 3, 17, 100, 28, 60, 50, 92, 235, 218, 57, 73, 119, 19, 101, 164, 192,
        161, 197, 106, 105, 73, 2, 3, 1, 0, 1]
    let pkBlob = DataBlob(pkVal)
    try {
        asyKeyGenerator.convertKey({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            Hilog.info(0, "", "convertKey result: success.")
        }, pkBlob, None)
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```

## Converting Binary Data to an ECC Key Pair

For the corresponding algorithm specifications, see [Asymmetric Key Generation and Conversion Specifications: ECC](./cj-crypto-asym-key-generation-conversion-spec.md#ecc).

1. Obtain the ECC public key or private key binary data and encapsulate it into a [DataBlob](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#class-datablob) object.

   Only one of the public key and private key can be passed in. This example passes in both the public key and private key.

2. Call [createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring), specifying the string parameter 'ECC256', to create an asymmetric key generator (AsyKeyGenerator) with key algorithm ECC and key length 256 bits.

3. Call [convertKey](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-convertkeyasynccallbackkeypairoptiondatabloboptiondatablob), passing in the public key binary data and private key binary data to generate an asymmetric key object (KeyPair).

The following example uses converting an ECC key pair:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.AsyncCallback
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testConvertECCKey() {
    let pubKeyArray: Array<UInt8> = [48, 89, 48, 19, 6, 7, 42, 134, 72, 206, 61, 2, 1, 6, 8, 42, 134, 72, 206, 61, 3, 1, 7, 3, 66, 0, 4,
        83, 96, 142, 9, 86, 214, 126, 106, 247, 233, 92, 125, 4, 128, 138, 105, 246, 162, 215, 71, 81, 58, 202, 121, 26,
        105, 211, 55, 130, 45, 236, 143, 55, 16, 248, 75, 167, 160, 167, 106, 2, 152, 243, 44, 68, 66, 0, 167, 99, 92,
        235, 215, 159, 239, 28, 106, 124, 171, 34, 145, 124, 174, 57, 92]
    let priKeyArray: Array<UInt8> = [48, 49, 2, 1, 1, 4, 32, 115, 56, 137, 35, 207, 0, 60, 191, 90, 61, 136, 105, 210, 16, 27, 4, 171,
        57, 10, 61, 123, 40, 189, 28, 34, 207, 236, 22, 45, 223, 10, 189, 160, 10, 6, 8, 42, 134, 72, 206, 61, 3, 1, 7]
    let pubKeyBlob = DataBlob(pubKeyArray)
    let priKeyBlob = DataBlob(priKeyArray)
    let generator = createAsyKeyGenerator("ECC256")
    try {
        generator.convertKey({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            Hilog.info(0, "", "convertKey result: success.")
        }, pubKeyBlob, priKeyBlob)
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```

## Converting Binary Data to an SM2 Key Pair

For the corresponding algorithm specifications, see [Asymmetric Key Generation and Conversion Specifications: SM2](./cj-crypto-asym-key-generation-conversion-spec.md#sm2).

1. Obtain the SM2 public key or private key binary data and encapsulate it into a [DataBlob](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#class-datablob) object.

   Only one of the public key and private key can be passed in. This example passes in both the public key and private key.

2. Call [createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring), specifying the string parameter 'SM2_256', to create an asymmetric key generator (AsyKeyGenerator) with key algorithm SM2 and key length 256 bits.

3. Call [convertKey](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-convertkeyasynccallbackkeypairoptiondatabloboptiondatablob), passing in the public key and private key binary data to generate an asymmetric key object (KeyPair).

The following example uses converting an SM2 key pair:

<!-- compile -->

```cangjie
import kit.CangjieKit.AsyncCallback
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testConvertSM2Key() {
    let pubKeyArray: Array<UInt8> = [48, 89, 48, 19, 6, 7, 42, 134, 72, 206, 61, 2, 1, 6, 8, 42, 129, 28, 207, 85, 1, 130, 45, 3, 66, 0,
        4, 90, 3, 58, 157, 190, 248, 76, 7, 132, 200, 151, 208, 112, 230, 96, 140, 90, 238, 211, 155, 128, 109, 248, 40,
        83, 214, 78, 42, 104, 106, 55, 148, 249, 35, 61, 32, 221, 135, 143, 100, 45, 97, 194, 176, 52, 73, 136, 174, 40,
        70, 70, 34, 103, 103, 161, 99, 27, 187, 13, 187, 109, 244, 13, 7]
    let priKeyArray: Array<UInt8> = [48, 49, 2, 1, 1, 4, 32, 54, 41, 239, 240, 63, 188, 134, 113, 31, 102, 149, 203, 245, 89, 15, 15, 47,
        202, 170, 60, 38, 154, 28, 169, 189, 100, 251, 76, 112, 223, 156, 159, 160, 10, 6, 8, 42, 129, 28, 207, 85, 1,
        130, 45]
    let pubKeyBlob = DataBlob(pubKeyArray)
    let priKeyBlob = DataBlob(priKeyArray)
    let generator = createAsyKeyGenerator("SM2_256")
    try {
        generator.convertKey({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            Hilog.info(0, "", "convertKey result: success.")
        }, pubKeyBlob, priKeyBlob)
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```
