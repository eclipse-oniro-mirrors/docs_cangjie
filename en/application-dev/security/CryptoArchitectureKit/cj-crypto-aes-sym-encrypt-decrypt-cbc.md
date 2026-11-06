# AES Symmetric Key Encryption and Decryption (CBC Mode)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

For corresponding algorithm specifications, please refer to [Symmetric Key Encryption/Decryption Algorithm Specifications: AES](./cj-crypto-sym-encrypt-decrypt-spec.md#aes).

## Encryption

1. Call [createSymKeyGenerator](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) and [generateSymKey](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-generatesymkey) to generate a symmetric key (SymKey) with AES algorithm and 128-bit key length.

   For guidance on generating AES symmetric keys, developers can refer to the example below, combined with [Symmetric Key Generation and Conversion Specifications: AES](./cj-crypto-sym-key-generation-conversion-spec.md#aes) and [Random Symmetric Key Generation](./cj-crypto-generate-sym-key-randomly.md). Note that reference documents may have parameter differences from the current example—please distinguish carefully when reading.

2. Call [createCipher](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'AES128|CBC|PKCS7' to create a Cipher instance with AES128 symmetric key type, CBC block mode, and PKCS7 padding mode for encryption operations.

3. Call [init](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to encryption (CryptoMode.EncryptMode), specify the encryption key (SymKey), and initialize the encryption Cipher instance with CBC mode parameters (IvParamsSpec).

4. For short encryption content, you can skip calling `update` and directly call [doFinal](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the encrypted data.

## Decryption

1. Call [createCipher](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createcipherstring) with the string parameter 'AES128|CBC|PKCS7' to create a Cipher instance with AES128 symmetric key type, CBC block mode, and PKCS7 padding mode for decryption operations.

2. Call [init](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to set the mode to decryption (CryptoMode.DecryptMode), specify the decryption key (SymKey), and initialize the decryption Cipher instance with CBC mode parameters (IvParamsSpec).

3. For short decryption content, you can skip calling `update` and directly call [doFinal](../../reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinaldatablob) to obtain the decrypted data.

## Example

Synchronous method example:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

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
    cipher.initialize(CryptoMode.EncryptMode, symKey, iv)
    let cipherData = cipher.doFinal(plainText)
    return cipherData
}

// Decrypt message.
func decryptMessage(symKey: SymKey, cipherText: DataBlob) {
    let decoder = createCipher('AES128|CBC|PKCS7')
    decoder.initialize(CryptoMode.DecryptMode, symKey, iv)
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
        Hilog.error(0,"","AES CBC ${e}, error code: ${e.code}")
    }
}
```