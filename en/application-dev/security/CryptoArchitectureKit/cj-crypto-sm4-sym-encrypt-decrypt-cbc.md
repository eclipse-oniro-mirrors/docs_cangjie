# Using SM4 Symmetric Key (CBC Mode) for Encryption and Decryption

For the corresponding algorithm specifications, please refer to [Symmetric Key Encryption/Decryption Algorithm Specifications: SM4](./cj-crypto-sym-encrypt-decrypt-spec.md#sm4).

## Encryption

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) to generate a symmetric key (SymKey) with SM4 as the key algorithm and a key length of 128 bits.

    For guidance on generating an SM4 symmetric key, developers can refer to the example below, combined with [Symmetric Key Generation and Conversion Specifications: SM4](./cj-crypto-sym-key-generation-conversion-spec.md#sm4) and [Random Symmetric Key Generation](./cj-crypto-generate-sym-key-randomly.md). Note that there may be parameter differences between the reference documents and the current example, so please pay attention to these distinctions when reading.

2. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'SM4_128|CBC|PKCS7' to create a Cipher instance for encryption operations, specifying SM4_128 as the symmetric key type, CBC as the block mode, and PKCS7 as the padding mode.

3. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to encryption (CryptoMode.EncryptMode), specify the encryption key (SymKey), and provide the encryption parameters (IvParamsSpec) corresponding to CBC mode, thereby initializing the encryption Cipher instance.

4. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update the data (plaintext).

    - For small amounts of data, you can directly call doFinal after init.
    - For large amounts of data, you can call update multiple times, i.e., perform segmented encryption/decryption.

5. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the encrypted data.

    Since the data has already been passed via update, pass None for the data parameter here.

## Decryption

1. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'SM4_128|CBC|PKCS7' to create a Cipher instance for decryption operations, specifying SM4_128 as the symmetric key type, CBC as the block mode, and PKCS7 as the padding mode.

2. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to decryption (CryptoMode.DecryptMode), specify the decryption key (SymKey), and provide the decryption parameters (IvParamsSpec) corresponding to CBC mode, thereby initializing the decryption Cipher instance.

3. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update the data (ciphertext).

4. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the decrypted data.

## Example

The synchronous method example is as follows:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.hilog.Hilog
import ohos.business_exception.BusinessException

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
    let cipher = createCipher('SM4_128|CBC|PKCS7')
    cipher.initialize(CryptoMode.EncryptMode, symKey, Some(iv))
    let cipherData = cipher.doFinal(plainText)
    return cipherData
}

// Decrypt message.
func decryptMessage(symKey: SymKey, cipherText: DataBlob) {
    let decoder = createCipher('SM4_128|CBC|PKCS7')
    decoder.initialize(CryptoMode.DecryptMode, symKey, Some(iv))
//    decoder.`init`(DECRYPT_MODE, symKey, iv)
    let decryptData = decoder.doFinal(cipherText)
    return decryptData
}

func genSymKeyByData(symKeyData: Array<UInt8>) {
    let symKeyBlob: DataBlob = DataBlob(symKeyData)
    let aesGenerator = createSymKeyGenerator('SM4_128')
    let symKey = aesGenerator.convertKey(symKeyBlob)
    Hilog.info(0, '', 'convertKey success')
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
            Hilog.info(0, '', 'decrypt ok')
            Hilog.info(0, '', 'decrypt plainText: ' + String.fromUtf8(decryptText.data))
        } else {
            Hilog.error(0, '', 'decrypt failed')
        }
    } catch (e: BusinessException) {
        Hilog.error(0, '', "SM4 ${e}, error code: ${e.code}")
    }
}
```