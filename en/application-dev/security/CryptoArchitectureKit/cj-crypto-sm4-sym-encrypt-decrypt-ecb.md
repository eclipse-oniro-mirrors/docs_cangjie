# Using SM4 Symmetric Key (ECB Mode) for Encryption and Decryption

For corresponding algorithm specifications, please refer to [Symmetric Key Encryption/Decryption Algorithm Specifications: SM4](./cj-crypto-sym-encrypt-decrypt-spec.md#sm4).

## Encryption

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) to generate a symmetric key (SymKey) with SM4 as the key algorithm and 128-bit key length.

    For guidance on generating an SM4 symmetric key, developers can refer to the example below and consult [Symmetric Key Generation and Conversion Specifications: SM4](./cj-crypto-sym-key-generation-conversion-spec.md#sm4) and [Random Symmetric Key Generation](./cj-crypto-generate-sym-key-randomly.md). Note that reference documents may have parameter differences from the current example—please pay attention to these distinctions when reading.

2. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'SM4_128|ECB|PKCS7' to create a Cipher instance configured for SM4_128 symmetric key type, ECB block mode, and PKCS7 padding mode, which will be used to perform encryption.

3. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to encryption (CryptoMode.EncryptMode), specify the encryption key (SymKey), and initialize the encryption Cipher instance.

    ECB mode has no encryption parameters, so pass None directly.

4. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update the data (plaintext).

    - For small data volumes, you can directly call doFinal after initialization.
    - For large data volumes, you can call update multiple times to perform segmented encryption/decryption.

5. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the encrypted data.

    Since the data has already been passed via update, pass None here for data.

## Decryption

1. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'SM4_128|ECB|PKCS7' to create a Cipher instance configured for SM4_128 symmetric key type, ECB block mode, and PKCS7 padding mode, which will be used to perform decryption.

2. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to decryption (CryptoMode.DecryptMode), specify the decryption key (SymKey), and initialize the decryption Cipher instance. ECB mode has no encryption parameters, so pass None directly.

3. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update the data (ciphertext).

4. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the decrypted data.

## Example

The synchronous method example is as follows:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

// Encrypt message.
func encryptMessage(symKey: SymKey, plainText: DataBlob) {
    let cipher = createCipher('SM4_128|ECB|PKCS7')
    cipher.initialize(CryptoMode.EncryptMode, symKey, None)
    let cipherData = cipher.doFinal(plainText)
    return cipherData
}

// Decrypt message.
func decryptMessage(symKey: SymKey, cipherText: DataBlob) {
    let decoder = createCipher('SM4_128|ECB|PKCS7')
    decoder.initialize(CryptoMode.DecryptMode, symKey, None)
    let decryptData = decoder.doFinal(cipherText)
    return decryptData
}

func genSymKeyByData(symKeyData: Array<UInt8>) {
    let symKeyBlob: DataBlob = DataBlob(symKeyData)
    let sm4Generator = createSymKeyGenerator('SM4_128')
    let symKey = sm4Generator.convertKey(symKeyBlob)
    Hilog.info(0,"","convertKey success")
    return symKey
}

func test() {
    try {
        let keyData: Array<UInt8> = [7, 154, 52, 176, 4, 236, 150, 43, 237, 9, 145, 166, 141, 174, 224, 131]
        let symKey = genSymKeyByData(keyData)
        let message = "This is a test"
        let plainText: DataBlob = DataBlob(message.toArray())
        let encryptText = encryptMessage(symKey, plainText)
        let decryptText = decryptMessage(symKey, encryptText)
        if (plainText.data.toString() == decryptText.data.toString()) {
            Hilog.info(0,"",'decrypt ok')
            Hilog.info(0,"",'decrypt plainText: ' + String.fromUtf8(decryptText.data))
        } else {
            Hilog.error(0,"",'decrypt failed')
        }
    } catch (e: BusinessException) {
        Hilog.error(0,"","SM4 ${e}, error code: ${e.code}")
    }
}
```