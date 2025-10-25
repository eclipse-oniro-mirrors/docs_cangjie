# Using AES Symmetric Key (CCM Mode) for Encryption and Decryption

For the corresponding algorithm specifications, please refer to [Symmetric Key Encryption/Decryption Algorithm Specifications: AES](./cj-crypto-sym-encrypt-decrypt-spec.md#aes).

## Encryption

1. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) and [generateSymKey](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatesymkey) to generate a symmetric key (SymKey) with AES as the key algorithm and 128-bit key length.

   For guidance on generating AES symmetric keys, developers can refer to the example below, combined with [Symmetric Key Generation and Conversion Specifications: AES](./cj-crypto-sym-key-generation-conversion-spec.md#aes) and [Random Symmetric Key Generation](./cj-crypto-generate-sym-key-randomly.md). Note that reference documents may have parameter differences from the current example—please pay attention to distinctions when reading.

2. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring), specifying the string parameter 'AES128|CCM' to create a Cipher instance with AES128 as the symmetric key type and CCM as the block mode, which will be used to perform encryption.

3. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec), set the mode to encryption (CryptoMode.ENCRYPT_MODE), specify the encryption key (SymKey) and the encryption parameters for CCM mode (CcmParamsSpec), and initialize the encryption Cipher instance.

4. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) to update data (plaintext).

   Currently, there is no length limit for a single update operation. Developers can determine how to call update based on the data volume.

   > **Note:**
   > CCM mode does not support segmented encryption/decryption.

5. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the encrypted data.
   Since data has already been passed via update, pass `None` for the data parameter here.

6. Read [CcmParamsSpec.authTag](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#struct-ccmparamsspec) as the authentication information for decryption.

   In CCM mode, the algorithm library currently only supports 12-byte authTag as the authentication information for decryption initialization. In this example, authTag is exactly 12 bytes.

## Decryption

1. Call [createCipher](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring), specifying the string parameter 'AES128|CCM' to create a Cipher instance with AES128 as the symmetric key type and CCM as the block mode, which will be used to perform decryption.

2. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec), set the mode to decryption (CryptoMode.DECRYPT_MODE), specify the decryption key (SymKey) and the decryption parameters for CCM mode (CcmParamsSpec), and initialize the decryption Cipher instance.

3. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the decrypted data.

## Example

Synchronous method example:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*

func genCcmParamsSpec() {
    let rand: Random = createRandom()
    let ivBlob: DataBlob = rand.generateRandom(7)
    let aadBlob: DataBlob = rand.generateRandom(8)
    let dataTag: Array<UInt8> = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0] // 12 bytes
    let tagBlob: DataBlob = DataBlob(dataTag)
    // In CCM mode, authTag is obtained from the doFinal result during encryption and passed to the params parameter of the init function during decryption.
    let ccmParamsSpec: CcmParamsSpec = CcmParamsSpec("CcmParamsSpec", ivBlob, aadBlob, tagBlob)
    return ccmParamsSpec
}

var ccmParams = genCcmParamsSpec()
// Encrypt message.
func encryptMessage(symKey: SymKey, plainText: DataBlob) {
    let cipher = createCipher('AES128|CCM')
    cipher.`init`(ENCRYPT_MODE, symKey, ccmParams)
    let encryptUpdate = cipher.update(plainText);
    // In CCM mode, pass None to doFinal during encryption to obtain tag data and update it to the ccmParams object.
    ccmParams.authTag = cipher.doFinal(None);
    return encryptUpdate
}

// Decrypt message.
func decryptMessage(symKey: SymKey, cipherText: DataBlob) {
    let decoder = createCipher('AES128|CCM')
    decoder.`init`(DECRYPT_MODE, symKey, ccmParams)
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
```