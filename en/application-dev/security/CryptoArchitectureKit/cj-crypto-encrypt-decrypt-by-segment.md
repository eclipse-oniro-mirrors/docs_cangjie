# Segment Encryption/Decryption Instructions

During the encryption/decryption process, the algorithm library imposes no size restrictions on single or cumulative data input. However, when handling large data volumes (e.g., exceeding 2MB), developers are advised to segment the data and perform segmented encryption/decryption to improve efficiency.

## Symmetric Encryption/Decryption

For symmetric key segmented encryption/decryption, implement it by calling the [update](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-updatedatablob) function.

Developers can customize the data volume for each input (e.g., `updateLength` in the example) by making multiple calls to the `update` interface to pass data.

The current maximum supported length for a single input is `INT_MAX` (the maximum length of the `Uint8Array` type).

**Development Example:** [Segmented AES Symmetric Key Encryption/Decryption (GCM Mode)](./cj-crypto-aes-sym-encrypt-decrypt-gcm-by-segment.md)

**Development Example:** [Segmented SM4 Symmetric Key Encryption/Decryption (GCM Mode)](./cj-crypto-sm4-sym-encrypt-decrypt-gcm-by-segment.md)

## Asymmetric Encryption/Decryption

Asymmetric encryption/decryption does not support the `update` operation. Simply call [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) to complete the process.

Segmented encryption for asymmetric keys refers to cases where the plaintext exceeds the supported data length for single encryption (specific lengths can be found in [Asymmetric Key Encryption/Decryption Algorithm Specifications](./cj-crypto-asym-encrypt-decrypt-spec.md)). In such scenarios, the data to be encrypted must be divided into appropriately sized segments, with each segment undergoing encryption—i.e., creating a `Cipher` object and then calling the [init](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#func-initcryptomode-key-paramsspec) interface.

Strictly speaking, this involves split-data encryption/decryption, where the length of data per input is related to the key specifications.

- **RSA**: The rules for input data vary depending on the padding mode. Refer to [RSA Algorithm Specifications](./cj-crypto-asym-encrypt-decrypt-spec.md#rsa) to determine the permissible data length per input.
- **SM2**: Encryption length must adhere to fixed specifications. For details, see [SM2 Algorithm Specifications](./cj-crypto-asym-encrypt-decrypt-spec.md#sm2).

## Frequently Asked Questions

In segmented encryption/decryption, is the data volume per update related to the encryption mode?

   The data volume per update is customizable by developers and is unrelated to the encryption mode.

   Different encryption modes only affect encryption/decryption parameters. Each mode uses distinct parameters; specifics can be found in [ParamsSpec](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#interface-paramsspec).