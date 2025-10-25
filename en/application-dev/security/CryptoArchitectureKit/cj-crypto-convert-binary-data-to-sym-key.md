# Converting Specified Binary Data to Symmetric Keys

Taking 3DES and HMAC as examples, this document describes how to generate a symmetric key (SymKey) from specified binary data, i.e., converting external or stored binary data into a key object of the cryptographic library, which can be used for subsequent operations such as encryption and decryption.

## Converting Specified Binary Data to 3DES Key

For corresponding algorithm specifications, refer to [Symmetric Key Generation and Conversion Specifications: 3DES](./cj-crypto-sym-key-generation-conversion-spec.md#3des).

1. Obtain 3DES binary key data and encapsulate it into a [DataBlob](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#struct-datablob) object.

2. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) with the string parameter '3DES192' to create a symmetric key generator (SymKeyGenerator) for the 3DES algorithm with a key length of 192 bits.

3. Call [convertKey](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-convertkeydatablob) to generate a symmetric key object (SymKey) from the specified binary key data.

4. Call [getEncoded](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded) to obtain the binary data of the key object.

Example of generating a 3DES key:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*

func genKeyMaterialBlob(): DataBlob {
    let arr: Array<UInt8> = [0xba, 0x3d, 0xc2, 0x71, 0x21, 0x1e, 0x30, 0x56, 0xad, 0x47, 0xfc, 0x5a, 0x46, 0x39, 0xee,
        0x7c, 0xba, 0x3b, 0xc2, 0x71, 0xab, 0xa0, 0x30, 0x72] // Key length is 192 bits (24 bytes).
    return DataBlob(arr)
}

func testConvertSymKey() {
    // Create SymKeyGenerator instance.
    let symKeyGenerator = createSymKeyGenerator('3DES192')
    // Generate symmetric key from specified data.
    let keyMaterialBlob = genKeyMaterialBlob()
    let key = symKeyGenerator.convertKey(keyMaterialBlob)
    let encodedKey = key.getEncoded() // Get binary data of symmetric key and output as byte array. Length is 24 bytes.
    AppLog.info('key getEncoded hex ${encodedKey.data}')
}
```

## Converting Specified Binary Data to HMAC Key

For corresponding algorithm specifications, refer to [Symmetric Key Generation and Conversion Specifications: HMAC](./cj-crypto-sym-key-generation-conversion-spec.md#hmac).

1. Obtain HMAC binary key data and encapsulate it into a DataBlob object.

2. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) with the string parameter 'HMAC' to create a symmetric key generator (SymKeyGenerator) for the HMAC algorithm with a key length between [1, 32768] bits.

3. Call [convertKey](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-convertkeydatablob) to generate a symmetric key object (SymKey) from the specified binary key data.

4. Call [getEncoded](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getencoded) to obtain the binary data of the key object.

Example of generating an HMAC key:

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*

func testConvertKey() {
    // Symmetric key length is 64 bytes (512 bits).
    let keyMessage = '12345678abcdefgh12345678abcdefgh12345678abcdefgh12345678abcdefgh'
    let keyBlob: DataBlob = DataBlob(keyMessage.toArray())
    let symKeyGenerator = createSymKeyGenerator('HMAC')
    let key = symKeyGenerator.convertKey(keyBlob)
    let encodedKey = key.getEncoded()
    AppLog.info('key encoded data：${encodedKey.data}')
}
```