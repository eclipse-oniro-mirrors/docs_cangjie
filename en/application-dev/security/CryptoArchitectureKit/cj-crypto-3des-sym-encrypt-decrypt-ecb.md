# 3DES Symmetric Key Encryption and Decryption (ECB Mode)

For the corresponding algorithm specifications, please refer to [Symmetric Key Encryption and Decryption Algorithm Specifications: 3DES](./cj-crypto-sym-encrypt-decrypt-spec.md#3des).

## Encryption

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) and [convertKey](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-convertkeydatablob) to generate a symmetric key (SymKey) with the 3DES algorithm and a key length of 192 bits.

   For guidance on generating a 3DES symmetric key, developers can refer to the example below, along with [Symmetric Key Generation and Conversion Specifications: 3DES](./cj-crypto-sym-key-generation-conversion-spec.md#3des) and [Convert Binary Data to Symmetric Key](./cj-crypto-convert-binary-data-to-sym-key.md). Note that there may be parameter differences between the reference documents and the current example, so please pay attention to these distinctions when reading.

2. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter '3DES192|ECB|PKCS7' to create a Cipher instance for encryption operations, specifying the symmetric key type as 3DES192, block mode as ECB, and padding mode as PKCS7.

3. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to encryption (CryptoMode.ENCRYPT_MODE), specify the encryption key (SymKey), and initialize the encryption Cipher instance.

   ECB mode does not require encryption parameters, so pass None directly.

4. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update the data (plaintext).

   - For small amounts of data, you can directly call doFinal after init.
   - For large amounts of data, you can call update multiple times, i.e., perform segmented encryption/decryption.
   - The threshold for data size can be determined by the user. For example, use update for data larger than 20 bytes.

5. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the encrypted data.

   Since the data has already been passed via update, pass None here for data.

## Decryption

1. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter '3DES192|ECB|PKCS7' to create a Cipher instance for decryption operations, specifying the symmetric key type as 3DES192, block mode as ECB, and padding mode as PKCS7.

2. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to decryption (CryptoMode.DECRYPT_MODE), specify the decryption key (SymKey), and initialize the decryption Cipher instance. ECB mode does not require encryption parameters, so pass None directly.

3. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update the data (ciphertext).

4. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the decrypted data.

## Example

A synchronous method example is as follows:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*

// Encrypt a message.
func encryptMessage(symKey: SymKey, plainText: DataBlob) {
    let cipher = createCipher('3DES192|ECB|PKCS7')
    cipher.`init`(ENCRYPT_MODE, symKey, None)
    let encryptData = cipher.doFinal(plainText)
    return encryptData
}

// Decrypt a message.
func decryptMessage(symKey: SymKey, cipherText: DataBlob) {
    let decoder = createCipher('3DES192|ECB|PKCS7')
    decoder.`init`(DECRYPT_MODE, symKey, None)
    let decryptData = decoder.doFinal(cipherText)
    return decryptData
}

func genSymKeyByData(symKeyData: Array<UInt8>) {
    let symKeyBlob: DataBlob = DataBlob(symKeyData)
    let symGenerator = createSymKeyGenerator('3DES192')
    let symKey = symGenerator.convertKey(symKeyBlob)
    AppLog.info('convertKey success')
    return symKey
}

func test() {
    let keyData: Array<UInt8> = [238, 249, 61, 55, 128, 220, 183, 224, 139, 253, 248, 239, 239, 41, 71, 25, 235, 206,
        230, 162, 249, 27, 234, 114]
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
}
```