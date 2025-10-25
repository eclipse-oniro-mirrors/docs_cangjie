# Using AES Symmetric Key (ECB Mode) for Encryption and Decryption

For corresponding algorithm specifications, please refer to [Symmetric Key Encryption/Decryption Algorithm Specifications: AES](./cj-crypto-sym-encrypt-decrypt-spec.md#aes).

## Encryption

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) to generate a symmetric key (SymKey) with AES as the key algorithm and a key length of 128 bits.

   For guidance on generating an AES symmetric key, developers can refer to the example below, along with [Symmetric Key Generation and Conversion Specifications: AES](./cj-crypto-sym-key-generation-conversion-spec.md#aes) and [Random Symmetric Key Generation](./cj-crypto-generate-sym-key-randomly.md). Note that there may be differences in input parameters between the reference documents and the current example, so please pay attention when reading.

2. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'AES128|ECB|PKCS7' to create a Cipher instance with AES128 as the symmetric key type, ECB as the block mode, and PKCS7 as the padding mode, which will be used to perform encryption operations.

3. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to encryption (CryptoMode.EncryptMode), specify the encryption key (SymKey), and initialize the encryption Cipher instance. No additional parameters are required for ECB mode.

4. If the content to be encrypted is short, you can skip calling `update` and directly call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the encrypted data.

## Decryption

1. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'AES128|ECB|PKCS7' to create a Cipher instance with AES128 as the symmetric key type, ECB as the block mode, and PKCS7 as the padding mode, which will be used to perform decryption operations.

2. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to decryption (CryptoMode.DecryptMode), specify the decryption key (SymKey), and initialize the decryption Cipher instance. No additional parameters are required for ECB mode.

3. If the content to be decrypted is short, you can skip calling `update` and directly call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the decrypted data.

## Example

The synchronous method example is as follows:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.business_exception.BusinessException
import ohos.hilog.Hilog

// Encrypt a message.
func encryptMessage(symKey: SymKey, plainText: DataBlob) {
    let cipher = createCipher('AES128|ECB|PKCS7')
    cipher.initialize(CryptoMode.EncryptMode, symKey, None) // No additional parameters needed for ECB mode.
    let cipherData = cipher.doFinal(plainText)
    return cipherData
}

// Decrypt a message.
func decryptMessage(symKey: SymKey, cipherText: DataBlob) {
    let decoder = createCipher('AES128|ECB|PKCS7')
    decoder.initialize(CryptoMode.DecryptMode, symKey, None) // No additional parameters needed for ECB mode.
    let decryptData = decoder.doFinal(cipherText)
    return decryptData
}

func genSymKeyByData(symKeyData: Array<UInt8>) {
    let symKeyBlob: DataBlob = DataBlob(symKeyData)
    let aesGenerator = createSymKeyGenerator('AES128')
    let symKey = aesGenerator.convertKey(symKeyBlob)
    Hilog.info(0,"",'convertKey success')
    return symKey
}

func test() {
    try {
        let keyData: Array<UInt8> = [83, 217, 231, 76, 28, 113, 23, 219, 250, 71, 209, 210, 205, 97, 32, 159]
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
        Hilog.error(0,"","AES ECB ${e}, error code: ${e.code}")
    }
}
```