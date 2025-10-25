# Using SM4 Symmetric Key (GCM Mode) for Segmented Encryption and Decryption

For corresponding algorithm specifications, please refer to [Symmetric Key Encryption/Decryption Algorithm Specifications: SM4](./cj-crypto-sym-encrypt-decrypt-spec.md#sm4).

## Encryption

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) to generate a symmetric key (SymKey) with SM4 algorithm and 128-bit key length.

    For guidance on generating SM4 symmetric keys, developers can refer to the example below, combined with [Symmetric Key Generation and Conversion Specifications: SM4](./cj-crypto-sym-key-generation-conversion-spec.md#sm4) and [Random Symmetric Key Generation](./cj-crypto-generate-sym-key-randomly.md). Note that reference documents may have parameter differences from the current example, so please pay attention when reading.

2. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring), specifying the string parameter 'SM4_128|GCM|PKCS7', to create a Cipher instance with SM4_128 symmetric key type, GCM block mode, and PKCS7 padding mode for encryption operations.

3. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec), set the mode to encryption (CryptoMode.ENCRYPT_MODE), specify the encryption key (SymKey) and GCM mode parameters (GcmParamsSpec), and initialize the encryption Cipher instance.

4. Set the data input size to 20 bytes per call and repeatedly call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update data (plaintext).

    - There is currently no limit on the length of a single update. Developers can decide how to call update based on the data volume.
    - It is recommended that developers check if the update result is an empty array each time and concatenate the data when the result is not empty to form the complete ciphertext. This is because update results may vary under different specifications.

        - For ECB and CBC modes, encryption is always performed in blocks, and the encrypted block results from the current update are output. If the current update fills a block, ciphertext is output; otherwise, an empty array is returned, and the unencrypted data is concatenated with the next input to form a complete block. During doFinal, the remaining unencrypted data is padded according to the specified padding mode, and the remaining encrypted results are output. The same logic applies to decryption.

        - For stream encryption modes (e.g., CTR and OFB), the ciphertext length is usually equal to the plaintext length.

5. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the encrypted data.

    Since data has already been passed via update, pass None for data here.

6. Read [GcmParamsSpec](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#struct-gcmparamsspec).authTag as the authentication information for decryption.

    In GCM mode, the last 16 bytes of the encrypted data must be extracted as the authentication information for decryption initialization. In this example, authTag is exactly 16 bytes.

## Decryption

1. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring), specifying the string parameter 'SM4_128|GCM|PKCS7', to create a Cipher instance with SM4_128 symmetric key type, GCM block mode, and PKCS7 padding mode for decryption operations.

2. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec), set the mode to decryption (CryptoMode.DECRYPT_MODE), specify the decryption key (SymKey) and GCM mode parameters (GcmParamsSpec), and initialize the decryption Cipher instance.

3. Set the data input size to 20 bytes per call and repeatedly call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update data (ciphertext).

4. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the decrypted data.

## Example

The synchronous method example is as follows:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import std.collection.ArrayList

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
    cipher.`init`(ENCRYPT_MODE, symKey, gcmParams)
    let updateLength = 20 // Assume 20-byte segments for update (no actual requirement).
    let cipherText = ArrayList<UInt8>()
    let size = plainText.data.size
    for (i in 0..size : updateLength) {
        let len = if (i + updateLength > size) {
            size
        } else {
            i + updateLength
        }
        let updateMessage = plainText.data[i..len]
        let updateMessageBlob: DataBlob = DataBlob(updateMessage)
        // Segmented update.
        let updateOutput = cipher.update(updateMessageBlob)
        // Concatenate update results to form ciphertext (in some cases, doFinal results may also need concatenation,
        // depending on block mode and padding. In this GCM example, doFinal only contains authTag, not ciphertext).
        cipherText.add(all: updateOutput.data)
    }
    gcmParams.authTag = cipher.doFinal(None)
    let cipherBlob: DataBlob = DataBlob(cipherText.toArray())
    return cipherBlob
}

// Decrypt message.
func decryptMessage(symKey: SymKey, cipherText: DataBlob) {
    let decoder = createCipher('SM4_128|GCM|PKCS7')
    decoder.`init`(DECRYPT_MODE, symKey, gcmParams)
    let updateLength = 20 // Assume 20-byte segments for update (no actual requirement).
    let decryptText = ArrayList<UInt8>()
    let size = cipherText.data.size
    for (i in 0..size : updateLength) {
        let len = if (i + updateLength > size) {
            size
        } else {
            i + updateLength
        }
        let updateMessage = cipherText.data[i..len]
        let updateMessageBlob: DataBlob = DataBlob(updateMessage)
        // Segmented update.
        let updateOutput = decoder.update(updateMessageBlob)
        // Concatenate update results to form plaintext.
        decryptText.add(all: updateOutput.data)
    }
    decoder.doFinal(None)
    let decryptBlob: DataBlob = DataBlob(decryptText.toArray());
    return decryptBlob;
}

func genSymKeyByData(symKeyData: Array<UInt8>) {
    let symKeyBlob: DataBlob = DataBlob(symKeyData)
    let aesGenerator = createSymKeyGenerator('SM4_128')
    let symKey = aesGenerator.convertKey(symKeyBlob)
    AppLog.info('convertKey success')
    return symKey
}

func test() {
    let keyData: Array<UInt8> = [83, 217, 231, 76, 28, 113, 23, 219, 250, 71, 209, 210, 205, 97, 32, 159]
    let symKey = genSymKeyByData(keyData)
    let message = "aaaaa.....bbbbb.....ccccc.....ddddd.....eee" // Assume the message is 43 bytes (UTF-8 encoded).
    let plainText: DataBlob = DataBlob(message.toArray())
    let encryptText = encryptMessage(symKey, plainText)
    let decryptText = decryptMessage(symKey, encryptText)
    if (plainText.data.toString() == decryptText.data.toString()) {
        AppLog.info('decrypt ok')
        AppLog.info('decrypt plainText: ' + String.fromUtf8(decryptText.data))
    } else {
        AppLog.error('decrypt failed')
    }
}
```