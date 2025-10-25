# Random Symmetric Key Generation

Taking AES and SM4 as examples, randomly generate symmetric keys (SymKey) and obtain their binary data.

The symmetric key object can be used for subsequent encryption/decryption operations, while the binary data can be stored or transmitted.

## Random AES Key Generation

For corresponding algorithm specifications, refer to [Symmetric Key Generation and Conversion Specifications: AES](./cj-crypto-sym-key-generation-conversion-spec.md#aes).

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) with the string parameter 'AES256' to create a symmetric key generator (SymKeyGenerator) using AES algorithm with 256-bit key length.

2. Call [generateSymKey](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatesymkey) to randomly generate a symmetric key object (SymKey).

3. Call [getEncoded](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded) to obtain the binary data of the key object.

## Example: Random AES Key Generation

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.hilog.Hilog

func testSyncGenerateAesKey() {
    // Create SymKeyGenerator instance.
    let symKeyGenerator = createSymKeyGenerator('AES256')
    // Use the key generator to randomly generate a symmetric key.
    let promiseSymKey = symKeyGenerator.generateSymKey()
    // Get the binary data of the symmetric key, outputting a 256-bit key (32 bytes in length).
    let encodedKey = promiseSymKey.getEncoded()
    Hilog.info(0,"",'key hex: ${encodedKey.data}')
}
```

## Random SM4 Key Generation

For corresponding algorithm specifications, refer to [Symmetric Key Generation and Conversion Specifications: SM4](./cj-crypto-sym-key-generation-conversion-spec.md#sm4).

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) with the string parameter 'SM4_128' to create a symmetric key generator (SymKeyGenerator) using SM4 algorithm with 128-bit key length.
   If developers need to use other algorithms, please modify the string parameter here accordingly.

2. Call [generateSymKey](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatesymkey) to randomly generate a symmetric key object (SymKey).

3. Call [getEncoded](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded) to obtain the binary data of the key object.

## Example: Random SM4 Key Generation

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.hilog.Hilog

func testSyncGenerateSm4Key() {
    // Create SymKeyGenerator instance.
    let symKeyGenerator = createSymKeyGenerator('SM4_128')
    // Use the key generator to randomly generate a symmetric key.
    let promiseSymKey = symKeyGenerator.generateSymKey()
    // Get the binary data of the symmetric key, outputting a 128-bit key (16 bytes in length).
    let encodedKey = promiseSymKey.getEncoded()
    Hilog.info(0,"",'key hex: ${encodedKey.data}')
}
```