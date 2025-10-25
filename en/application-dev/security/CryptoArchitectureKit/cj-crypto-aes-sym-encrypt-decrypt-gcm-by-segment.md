# AES Symmetric Key (GCM Mode) Segmented Encryption and Decryption

For corresponding algorithm specifications, please refer to [Symmetric Key Encryption/Decryption Algorithm Specifications: AES](./cj-crypto-sym-encrypt-decrypt-spec.md#aes).

## Encryption

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) to generate a symmetric key (SymKey) with AES as the key algorithm and 128-bit key length.

   For guidance on generating an AES symmetric key, developers can refer to the example below, combined with [Symmetric Key Generation and Conversion Specifications: AES](./cj-crypto-sym-key-generation-conversion-spec.md#aes) and [Random Symmetric Key Generation](./cj-crypto-generate-sym-key-randomly.md). Note that reference documents may have parameter differences from the current example, so please distinguish carefully when reading.

2. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring), specifying the string parameter 'AES128|GCM|PKCS7' to create a Cipher instance with AES128 as the symmetric key type, GCM as the block mode, and PKCS7 as the padding mode for encryption operations.

3. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec), set the mode to encryption (CryptoMode.EncryptMode), specify the encryption key (SymKey) and the encryption parameters corresponding to GCM mode (GcmParamsSpec), and initialize the encryption Cipher instance.

4. Set the data input size to 20 bytes per call and call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) multiple times to update the data (plaintext).

   There is currently no limit on the length of a single update. Developers can decide how to call update based on the data volume.

      1) For example, in ECB and CBC modes, encryption is always performed in blocks, and the encrypted block results from this update are output. If the current update operation fills a block, ciphertext is output; otherwise, the update outputs an empty DataBlob, and the unencrypted data is concatenated with the next input data to form a block before output. During the final doFinal step, the remaining unencrypted data is padded according to the specified padding mode, and the remaining encryption results are output. The same logic applies to the update process during decryption.

      2) For stream encryption modes (e.g., CTR and OFB), the ciphertext length is usually equal to the plaintext length.

5. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the encrypted data.

   Since data has already been passed via update, pass None for the data parameter here.

6. Read [GcmParamsSpec](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#struct-gcmparamsspec).authTag as the authentication information for decryption.

   In GCM mode, the algorithm library currently only supports a 16-byte authTag as the authentication information for decryption initialization. In this example, the authTag happens to be 16 bytes.

## Decryption

1. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring), specifying the string parameter 'AES128|GCM|PKCS7' to create a Cipher instance with AES128 as the symmetric key type, GCM as the block mode, and PKCS7 as the padding mode for decryption operations.

2. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec), set the mode to decryption (CryptoMode.DecryptMode), specify the decryption key (SymKey) and the decryption parameters corresponding to GCM mode (GcmParamsSpec), and initialize the decryption Cipher instance.

3. Set the data input size to 20 bytes per call and call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) multiple times to update the data (ciphertext).

4. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the decrypted data.

## Example

The synchronous method example is as follows:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import std.collection.ArrayList
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
    let updateLength = 20 // Assume updating in segments of 20 bytes; there are no actual requirements.
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
        // Segment update.
        let updateOutput = cipher.update(updateMessageBlob)
        // Concatenate the update results to obtain the ciphertext (in some cases, the doFinal results may also need to be concatenated, depending on the block mode and padding mode. In this GCM mode example, doFinal only contains authTag and not ciphertext, so no concatenation is needed).
        cipherText.add(all: updateOutput.data)
    }
    gcmParams.authTag = cipher.doFinal(None)
    let cipherBlob: DataBlob = DataBlob(cipherText.toArray())
    return cipherBlob
}

// Decrypt message.
func decryptMessage(symKey: SymKey, cipherText: DataBlob) {
    let decoder = createCipher('AES128|GCM|PKCS7')
    decoder.initialize(CryptoMode.DecryptMode, symKey, gcmParams)
    let updateLength = 20 // Assume updating in segments of 20 bytes; there are no actual requirements.
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
        // Segment update.
        let updateOutput = decoder.update(updateMessageBlob)
        // Concatenate the update results to obtain the plaintext.
        decryptText.add(all: updateOutput.data)
    }
    decoder.doFinal(None)
    let decryptBlob: DataBlob = DataBlob(decryptText.toArray())
    return decryptBlob
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
    let message = "aaaaa.....bbbbb.....ccccc.....ddddd.....eee" // Assume the message is 43 bytes in total; after UTF-8 decoding, it remains 43 bytes.
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