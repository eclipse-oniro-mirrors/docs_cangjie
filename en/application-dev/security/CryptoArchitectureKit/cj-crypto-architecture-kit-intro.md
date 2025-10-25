# Introduction to Crypto Architecture Kit

The Crypto Architecture Kit provides functionalities related to encryption/decryption, signature generation/verification, message authentication codes, hashing, secure random number generation, key derivation, and more.

By abstracting the implementation differences of third-party cryptographic algorithm libraries, the Crypto Architecture Kit enables developers to quickly implement cryptographic operations through its algorithm framework services, without needing to account for variations in underlying third-party libraries.

## Basic Concepts

Before developing specific functionalities, developers should understand the following fundamental concepts.

- **Symmetric Key**

  Both encryption and decryption parties use the same key pair to perform data encryption and decryption operations. Specifically, the data sender uses an encryption key to process plaintext with a specific encryption algorithm, transforming it into complex ciphertext for transmission. The receiver must use the same key and the inverse algorithm to decrypt the ciphertext and recover the original readable plaintext.

- **Asymmetric Key**

  Asymmetric keys use two distinct keys—a public key and a private key—for cryptographic operations. The public key is openly shared, while the private key remains confidential.

  - For encryption/decryption operations: The public key is typically used to encrypt plaintext into ciphertext, and only the holder of the private key can decrypt the ciphertext.
  - For signature/verification operations: The private key is used to sign plaintext, and the public key holder can verify the signature data to confirm its integrity and detect tampering.

## Capabilities

The cryptographic algorithm library offers the following functionalities to developers, along with corresponding algorithm specifications and development guidelines. Please refer to these resources during development.

- [Key Generation and Conversion](./cj-crypto-key-generation-conversion-overview.md)
- [Encryption and Decryption](./cj-crypto-encryption-decryption-overview.md)
- [Message Digest Calculation](./cj-crypto-generate-message-digest-overview.md)
- [Message Authentication Code (MAC) Calculation](./cj-crypto-compute-mac.md)
- [Secure Random Number Generation](./cj-crypto-generate-random-number.md)

## Relationship with Other Kits

The cryptographic algorithm library framework only provides cryptographic operations for keys and does not include key management functionality. Therefore, when using the algorithm library, applications must manage their own keys. This is suitable for scenarios such as temporary session keys that reside only in memory or cases where the application implements secure key storage independently.

If your business requires system-provided key management (e.g., key storage), refer to the [Universal Keystore Kit (Key Management Service)](../UniversalKeystoreKit/cj-huks-overview.md).

## Constraints and Limitations

- The Crypto Architecture Kit does not support multi-threaded concurrent operations.
- Currently, the Crypto Architecture Kit only supports OpenSSL.
- While the Crypto Architecture Kit provides most commonly used algorithms, certain algorithms and specifications (e.g., MD5) are not suitable for high-security scenarios. Developers should select appropriate algorithms based on actual requirements.