# AES Symmetric Key Encryption and Decryption (GCM Mode)

For corresponding algorithm specifications, refer to [Symmetric Key Encryption and Decryption Algorithm Specifications: AES](./cj-crypto-sym-encrypt-decrypt-spec.md#aes).

## Encryption

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) to generate a symmetric key (SymKey) with AES as the key algorithm and 128-bit key length.

   For guidance on generating AES symmetric keys, developers can refer to the example below, combined with [Symmetric Key Generation and Conversion Specifications: AES](./cj-crypto-sym-key-generation-conversion-spec.md#aes) and [Random Symmetric Key Generation](./cj-crypto-generate-sym-key-randomly.md). Note that reference documents may have parameter differences from the current example, so please pay attention to distinctions when reading.

2. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'AES128|GCM|PKCS7' to create a Cipher instance for encryption operations, specifying AES128 as the symmetric key type, GCM as the block mode, and PKCS7 as the padding mode.

3. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to encryption (CryptoMode.EncryptMode), specify the encryption key (SymKey), and the encryption parameters for GCM mode (GcmParamsSpec) to initialize the encryption Cipher instance.

4. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update data (plaintext).

   There is currently no limit on the length of a single update. Developers can determine how to call update based on the data volume.

   - For small data volumes, doFinal can be called directly after init.
   - For large data volumes, update can be called multiple times, i.e., [Segmented Encryption and Decryption](./cj-crypto-aes-sym-encrypt-decrypt-gcm-by-segment.md).

5. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the encrypted data.
   Since data has already been passed via update, pass None for data here.

6. Read [GcmParamsSpec](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#struct-gcmparamsspec).authTag as the authentication information for decryption.
   In GCM mode, the algorithm library currently only supports a 16-byte authTag, which serves as the authentication information during decryption initialization. In this example, the authTag length is exactly 16 bytes.

## Decryption

1. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'AES128|GCM|PKCS7' to create a Cipher instance for decryption operations, specifying AES128 as the symmetric key type, GCM as the block mode, and PKCS7 as the padding mode.

2. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to decryption (CryptoMode.DecryptMode), specify the decryption key (SymKey), and the decryption parameters for GCM mode (GcmParamsSpec) to initialize the decryption Cipher instance.

3. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update data (ciphertext).

4. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the decrypted data.

## Example

Synchronous method example:

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
    let cipher = createCipher('AES128|GCM|PKCS7')
    cipher.initialize(CryptoMode.EncryptMode, symKey, gcmParams)
    let encryptUpdate = cipher.update(plainText)
    // In GCM mode, pass None to doFinal during encryption to obtain tag data and update it in the gcmParams object.
    gcmParams.authTag = cipher.doFinal(None)
    return encryptUpdate
}

// Decrypt message.
func decryptMessage(symKey: SymKey, cipherText: DataBlob) {
    let decoder = createCipher('AES128|GCM|PKCS7')
    decoder.initialize(CryptoMode.DecryptMode, symKey, gcmParams)
    let decryptUpdate = decoder.update(cipherText)
    decoder.doFinal(None)
    return decryptUpdate
}

func genSymKeyByData(symKeyData: Array<UInt8>) {
    let symKeyBlob: DataBlob = DataBlob(symKeyData)
    let aesGenerator = createSymKeyGenerator('AES128')
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