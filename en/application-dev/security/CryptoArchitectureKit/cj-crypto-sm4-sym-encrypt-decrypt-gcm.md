# Using SM4 Symmetric Key (GCM Mode) for Encryption and Decryption

For corresponding algorithm specifications, please refer to [Symmetric Key Encryption/Decryption Algorithm Specifications: SM4](./cj-crypto-sym-encrypt-decrypt-spec.md#sm4).

## Encryption

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) to generate a symmetric key (SymKey) with SM4 as the key algorithm and 128-bit key length.

    For guidance on generating an SM4 symmetric key, developers can refer to the example below, combined with [Symmetric Key Generation and Conversion Specifications: SM4](./cj-crypto-sym-key-generation-conversion-spec.md#sm4) and [Random Symmetric Key Generation](./cj-crypto-generate-sym-key-randomly.md). Note that reference documents may have parameter differences from the current example—please distinguish carefully when reading.

2. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'SM4_128|GCM|PKCS7' to create a Cipher instance for encryption operations, specifying SM4_128 as the symmetric key type, GCM as the block mode, and PKCS7 as the padding mode.

3. Call [initialize](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializecryptomode-key-paramsspec) to set the mode to encryption (CryptoMode.EncryptMode), specify the encryption key (SymKey), and configure the encryption parameters for GCM mode (GcmParamsSpec) to initialize the encryption Cipher instance.

4. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update the data (plaintext).

    There is no length limit for a single `update` call. Developers can determine how to call `update` based on the data volume:
    - For small data volumes, `doFinal` can be called directly after initialization.
    - For large data volumes, `update` can be called multiple times (i.e., segmented encryption/decryption).

5. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the encrypted data.

    Since the data has already been passed via `update`, `data` should be set to `None` here.

6. Read [GcmParamsSpec](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#struct-gcmparamsspec).authTag as the authentication tag for decryption.

    In GCM mode, the last 16 bytes of the encrypted data must be extracted as the authentication tag for decryption initialization. In this example, `authTag` is exactly 16 bytes.

## Decryption

1. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'SM4_128|GCM|PKCS7' to create a Cipher instance for decryption operations, specifying SM4_128 as the symmetric key type, GCM as the block mode, and PKCS7 as the padding mode.

2. Call [initialize](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initializecryptomode-key-paramsspec) to set the mode to decryption (CryptoMode.DecryptMode), specify the decryption key (SymKey), and configure the decryption parameters for GCM mode (GcmParamsSpec) to initialize the decryption Cipher instance.

3. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update the data (ciphertext).

4. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the decrypted data.

## Example

A synchronous method example is provided below:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import ohos.hilog.Hilog

func generateRandom(len: Int32) {
    let rand = createRandom()
    let generateRandSync = rand.generateRandom(len)
    return generateRandSync
}

func genGcmParamsSpec() {
    let ivBlob = generateRandom(12)
    let aadBlob: DataBlob = DataBlob([1, 2, 3, 4, 5, 6, 7, 8]) // 8 bytes
    let arr: Array<UInt8> = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] // 16 bytes
    let tagBlob: DataBlob = DataBlob() // The GCM authTag is obtained by doFinal() in encryption and passed in params of init() in decryption.
    let gcmParamsSpec: GcmParamsSpec = GcmParamsSpec("GcmParamsSpec", ivBlob, aadBlob, tagBlob)
    return gcmParamsSpec
}

var gcmParams = genGcmParamsSpec()
// Encrypt message.
func encryptMessage(symKey: SymKey, plainText: DataBlob) {
    let cipher = createCipher('SM4_128|GCM|PKCS7')
    cipher.initialize(CryptoMode.EncryptMode, symKey, gcmParams)
    let encryptUpdate = cipher.update(plainText)
    // In GCM mode, pass None to doFinal to obtain the tag data and update it in the gcmParams object.
    gcmParams.authTag = cipher.doFinal(None)
    return encryptUpdate
}

// Decrypt message.
func decryptMessage(symKey: SymKey, cipherText: DataBlob) {
    let decoder = createCipher('SM4_128|GCM|PKCS7')
    decoder.initialize(CryptoMode.DecryptMode, symKey, gcmParams)
    let decryptUpdate = decoder.update(cipherText)
    decoder.doFinal(None)
    return decryptUpdate;
}

func genSymKeyByData(symKeyData: Array<UInt8>) {
    let symKeyBlob: DataBlob = DataBlob(symKeyData)
    let aesGenerator = createSymKeyGenerator('SM4_128')
    let symKey = aesGenerator.convertKey(symKeyBlob)
    Hilog.info(0,"",'convertKey success')
    return symKey
}

func test() {
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
}
```