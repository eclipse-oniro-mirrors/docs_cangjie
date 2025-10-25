# AES Symmetric Key Encryption and Decryption (CBC Mode)

For corresponding algorithm specifications, please refer to [Symmetric Key Encryption and Decryption Algorithm Specifications: AES](./cj-crypto-sym-encrypt-decrypt-spec.md#aes).

## Encryption

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) and [generateSymKey](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatesymkey) to generate a symmetric key (SymKey) with AES algorithm and 128-bit key length.

   Developers can refer to the example below for generating AES symmetric keys, combined with [Symmetric Key Generation and Conversion Specifications: AES](./cj-crypto-sym-key-generation-conversion-spec.md#aes) and [Random Symmetric Key Generation](./cj-crypto-generate-sym-key-randomly.md). Note that reference documents may have parameter differences from the current example, so please pay attention when reading.

2. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'AES128|CBC|PKCS7' to create a Cipher instance with AES128 symmetric key type, CBC block mode, and PKCS7 padding mode for encryption operations.

3. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec), set the mode to encryption (CryptoMode.ENCRYPT_MODE), specify the encryption key (SymKey) and the encryption parameters for CBC mode (IvParamsSpec), and initialize the encryption Cipher instance.

4. For shorter content, you can skip calling update and directly call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the encrypted data.

## Decryption

1. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'AES128|CBC|PKCS7' to create a Cipher instance with AES128 symmetric key type, CBC block mode, and PKCS7 padding mode for decryption operations.

2. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec), set the mode to decryption (CryptoMode.DECRYPT_MODE), specify the decryption key (SymKey) and the decryption parameters for CBC mode (IvParamsSpec), and initialize the decryption Cipher instance.

3. For shorter content, you can skip calling update and directly call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the decrypted data.

## Example

Synchronous method example:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.base.BusinessException

func generateRandom(len: Int32) {
    let rand = createRandom()
    let generateRandSync = rand.generateRandom(len)
    return generateRandSync
}

func genIvParamsSpec() {
    let ivBlob = generateRandom(16)
    let ivParamsSpec: IvParamsSpec = IvParamsSpec("IvParamsSpec", ivBlob)
    return ivParamsSpec
}

let iv = genIvParamsSpec()
// Encrypt message.
func encryptMessage(symKey: SymKey, plainText: DataBlob) {
    let cipher = createCipher('AES128|CBC|PKCS7')
    cipher.`init`(ENCRYPT_MODE, symKey, iv)
    let cipherData = cipher.doFinal(plainText)
    return cipherData
}

// Decrypt message.
func decryptMessage(symKey: SymKey, cipherText: DataBlob) {
    let decoder = createCipher('AES128|CBC|PKCS7')
    decoder.`init`(DECRYPT_MODE, symKey, iv)
    let decryptData = decoder.doFinal(cipherText)
    return decryptData
}

func genSymKeyByData(symKeyData: Array<UInt8>) {
    let symKeyBlob: DataBlob = DataBlob(symKeyData)
    let aesGenerator = createSymKeyGenerator('AES128')
    let symKey = aesGenerator.convertKey(symKeyBlob)
    AppLog.info('convertKey success')
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
            AppLog.info('decrypt ok')
            AppLog.info('decrypt plainText: ' + String.fromUtf8(decryptText.data))
        } else {
            AppLog.error('decrypt failed')
        }
    } catch (e: BusinessException) {
        AppLog.error("AES CBC ${e}, error code: ${e.code}")
    }
}
```