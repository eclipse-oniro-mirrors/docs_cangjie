# Message Authentication Code Calculation

MAC (Message Authentication Code) enables integrity verification of messages by using a shared secret key between communicating parties to detect tampering or forgery attempts.

HMAC (Hash-based Message Authentication Code) is a hash-based message authentication code algorithm.

HMAC generates a fixed-length authentication code by taking both the shared secret key and the message as inputs through a specified digest algorithm, which is used to verify the integrity of transmitted messages. By incorporating the secret key into the message digest algorithm, HMAC ensures message authenticity.

## Supported Algorithms and Specifications

When creating HMAC message authentication codes, you must specify the HMAC specification using algorithms listed in the "Supported Types" column of the following table.

| Digest Algorithm | Supported Types | API Version |
| ---------------- | --------------- | ----------- |
| HASH | SHA1 | 12+ |
| HASH | SHA224 | 12+ |
| HASH | SHA256 | 12+ |
| HASH | SHA384 | 12+ |
| HASH | SHA512 | 12+ |
| HASH | SM3 | 12+ |
| HASH | MD5 | 12+ |

## Development Procedure

When passing data through the update interface, you can either [pass all data at once](#hmac-single-pass) or manually segment the data and [update in segments](#segmented-hmac). For the same data segment, whether segmented or not, the calculation results remain identical. For large datasets, developers can choose the appropriate method based on actual requirements.

Below are example codes for both approaches.

### HMAC (Single Pass)

1. Call [createMac](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createmacstring), specifying the SHA256 digest algorithm to generate a message authentication code instance (Mac).

2. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) and [convertKey](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-convertkeydatablob) to generate a symmetric key (SymKey) with HMAC as the key algorithm.
   For detailed guidance on symmetric key generation, refer to [Generate Symmetric Key from Binary Data](./cj-crypto-convert-binary-data-to-sym-key.md).

3. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initsymkey), specifying the shared symmetric key (SymKey) to initialize the Mac object.

4. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-1), passing custom message data for MAC calculation. There is no length restriction for single update operations.

5. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinal) to obtain the MAC calculation result.

6. Call [getMacLength](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getmaclength) to retrieve the MAC length in bytes.

### Example: Single-Pass Data Input for MAC Calculation

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*

func genSymKeyByData(symKeyData: Array<UInt8>) {
    let symKeyBlob: DataBlob = DataBlob(symKeyData)
    let aesGenerator = createSymKeyGenerator('HMAC')
    let symKey = aesGenerator.convertKey(symKeyBlob)
    AppLog.info('convertKey success')
    return symKey
}

func doHmacBySync() {
    // Decode string as Uint8Array using UTF-8, using a fixed 128-bit key (16 bytes)
    let keyData = "12345678abcdefgh".toArray()
    let key = genSymKeyByData(keyData)
    let macAlgName = 'SHA256' // Digest algorithm name
    let message = 'hmacTestMessgae' // Data for HMAC calculation
    let mac = createMac(macAlgName)
    mac.`init`(key)
    // For small datasets, perform single update with all data (no length restriction)
    mac.update(DataBlob(keyData))
    let macResult = mac.doFinal()
    AppLog.info('[Sync]HMAC result: ${macResult.data}')
    let macLen = mac.getMacLength()
    AppLog.info('HMAC len: ${macLen}')
}
```

### Segmented HMAC

1. Call [createMac](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createmacstring), specifying the SHA256 digest algorithm to generate a message authentication code instance (Mac).

2. Call [createSymKeyGenerator](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-createsymkeygeneratorstring) to generate a symmetric key (SymKey) with HMAC as the key algorithm.
   For detailed guidance on symmetric key generation, refer to [Generate Symmetric Key from Binary Data](./cj-crypto-convert-binary-data-to-sym-key.md).

3. Call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initsymkey), specifying the shared symmetric key (SymKey) to initialize the Mac object.

4. Pass custom message data, setting each update segment to 20 bytes. Call [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob-1) multiple times for MAC calculation.

5. Call [doFinal](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-dofinal) to obtain the MAC calculation result.

6. Call [getMacLength](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-getmaclength) to retrieve the MAC length in bytes.

### Example: Segmented Data Input for MAC Calculation

<!-- compile -->

```cangjie
import kit.CryptoArchitectureKit.*

func genSymKeyByData(symKeyData: Array<UInt8>) {
    let symKeyBlob: DataBlob = DataBlob(symKeyData)
    let aesGenerator = createSymKeyGenerator('HMAC')
    let symKey = aesGenerator.convertKey(symKeyBlob)
    AppLog.info('convertKey success')
    return symKey
}

func doHmacBySync() {
    // Decode string as Uint8Array using UTF-8, using a fixed 128-bit key (16 bytes)
    let keyData = "12345678abcdefgh".toArray()
    let key = genSymKeyByData(keyData)
    let macAlgName = 'SHA256' // Digest algorithm name
    let message = 'aaaaa.....bbbbb.....ccccc.....ddddd.....eee'.toArray() // Data for HMAC calculation
    let mac = createMac(macAlgName)
    mac.`init`(key)
    let updateLength = 20; // Assume 20-byte segments for update (no actual requirement)
    let size = message.size
    // For small datasets, perform single update with all data (no length restriction)
    for (i in 0..size : updateLength) {
        let len = if (i + updateLength > size) {
            size
        } else {
            i + updateLength
        }
        let updateMessage = message[i..len]
        let updateMessageBlob: DataBlob = DataBlob(updateMessage)
        mac.update(updateMessageBlob)
    }
    let macResult = mac.doFinal()
    AppLog.info('[Sync]HMAC result: ${macResult.data}')
    let macLen = mac.getMacLength()
    AppLog.info('HMAC len: ${macLen}')
}
```