# Randomly Generating an Asymmetric Key Pair

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Taking RSA and SM2 as examples, an asymmetric key pair (KeyPair) is randomly generated and its binary data is obtained.

The asymmetric key pair can be used for subsequent operations such as encryption and decryption, and the binary data can be used for storage or transmission.

## Randomly Generating an RSA Key Pair

For the corresponding algorithm specifications, see [Asymmetric Key Generation and Conversion Specifications: RSA](./cj-crypto-asym-key-generation-conversion-spec.md#rsa).

1. Call [createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring), specifying the string parameter 'RSA1024|PRIMES_2', to create an asymmetric key generator (AsyKeyGenerator) with RSA key type RSA1024 and 2 primes.

2. Call [generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair) to randomly generate an asymmetric key object (KeyPair).

   The KeyPair object includes the public key PubKey and the private key PriKey.

3. Call [PubKey.getEncoded](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded) and [PriKey.getEncoded](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded) respectively to obtain the binary data of the key objects.

The following example uses randomly generating an RSA key pair:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testGenerateRSAKeyPair() {
    let asyKeyGenerator = createAsyKeyGenerator("RSA1024|PRIMES_2")
    try {
        asyKeyGenerator.generateKeyPair({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            if (let Some(kp) <- keyPair) {
                let pubKey = kp.pubKey
                let priKey = kp.priKey
                // Obtain the binary data of the asymmetric key pair
                let pkBlob = pubKey.getEncoded()
                let skBlob = priKey.getEncoded()
                Hilog.info(0, "", "pk bin data: ${pkBlob.data}")
                Hilog.info(0, "", "sk bin data: ${skBlob.data}")
            }
        })
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```

## Randomly Generating an SM2 Key Pair

For the corresponding algorithm specifications, see [Asymmetric Key Generation and Conversion Specifications: SM2](./cj-crypto-asym-key-generation-conversion-spec.md#sm2).

1. Call [createAsyKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createasykeygeneratorstring), specifying the string parameter 'SM2_256', to create an asymmetric key generator (AsyKeyGenerator) with key algorithm SM2 and key length 256 bits.

2. Call [generateKeyPair](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatekeypairasynccallbackkeypair) to randomly generate an asymmetric key object (KeyPair).

   The KeyPair object includes the public key PubKey and the private key PriKey.

3. Call [PubKey.getEncoded](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded) and [PriKey.getEncoded](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded) respectively to obtain the binary data of the key objects.

The following example uses randomly generating an SM2 key pair:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func testGenerateSM2KeyPair() {
    let asyKeyGenerator = createAsyKeyGenerator("SM2_256")
    try {
        asyKeyGenerator.generateKeyPair({ err, keyPair =>
            if (let Some(e) <- err) {
                throw e
            }
            if (let Some(kp) <- keyPair) {
                let pubKey = kp.pubKey
                let priKey = kp.priKey
                // Obtain the binary data of the asymmetric key pair
                let pkBlob = pubKey.getEncoded()
                let skBlob = priKey.getEncoded()
                Hilog.info(0, "", "pk bin data: ${pkBlob.data}")
                Hilog.info(0, "", "sk bin data: ${skBlob.data}")
            }
        })
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "${e.message}")
    }
}
```
