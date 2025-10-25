# Symmetric Key Encryption/Decryption Algorithm Specifications

This section describes the algorithms currently supported by the system and their corresponding specifications.

For each algorithm, the supported encryption modes will be introduced in their respective algorithm specifications.

## AES

The algorithm library currently provides seven common encryption modes for [AES](./cj-crypto-sym-key-generation-conversion-spec.md#aes) encryption/decryption: ECB, CBC, OFB, CFB, CTR, GCM, and CCM. Different encryption modes require different encryption/decryption parameters. For details, refer to [ParamsSpec](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#interface-paramsspec).

Since AES is a block cipher algorithm, the block length is 128 bits. In practical applications, the last block of plaintext may be less than 128 bits (16 bytes). In such cases, data padding can be performed using different [padding modes](#padding-modes).

Since padding is required to reach the block size, both PKCS5 and PKCS7 in the actual algorithm library use the block size as the padding length, meaning AES encryption pads to 16 bytes.

> **Note:**
>
> - For ECB and CBC encryption modes, if the plaintext length is not an integer multiple of 128 bits, padding must be used to complete the block.
> - For CCM encryption mode, additional authenticated data (aad) must be specified, and its length must be between 1 byte and 2048 bytes.

Currently, AES encryption/decryption can be performed using string parameters. The "string parameter" is constructed by concatenating the "symmetric key type (encryption/decryption algorithm + key length)", "block mode", and "padding mode" with the "|" symbol. This is used to specify the algorithm specification when creating a symmetric encryption/decryption instance.

- As shown in the table below, only one item can be selected from each range (i.e., the content within []) to complete the string concatenation.

  Examples:
  
    - For an AES key with ECB block mode, 128-bit key length, and PKCS7 padding mode, the string parameter is "AES128|ECB|PKCS7".
    - For an AES key with CFB block mode, 256-bit key length, and NoPadding mode, the string parameter is "AES256|CFB|NoPadding".

  | Block Mode | Key Length (bit) | Padding Mode | API Version |
  | :-------- | :-------- | :-------- | :-------- |
  | ECB | [128\|192\|256] | [NoPadding\|PKCS5\|PKCS7] | 12+ |
  | CBC | [128\|192\|256] | [NoPadding\|PKCS5\|PKCS7] | 12+ |
  | CTR | [128\|192\|256] | [NoPadding\|PKCS5\|PKCS7] | 12+ |
  | OFB | [128\|192\|256] | [NoPadding\|PKCS5\|PKCS7] | 12+ |
  | CFB | [128\|192\|256] | [NoPadding\|PKCS5\|PKCS7] | 12+ |
  | GCM | [128\|192\|256] | [NoPadding\|PKCS5\|PKCS7] | 12+ |
  | CCM | [128\|192\|256] | [NoPadding\|PKCS5\|PKCS7] | 12+ |

- Starting from API version 12, symmetric encryption/decryption without key length specification is supported. When inputting the key type for encryption/decryption parameters, the key length can be omitted, and the encryption/decryption operation will depend on the actual input key length.

  Example: For an AES key with CFB block mode, no key length specified, and NoPadding mode, the string parameter is "AES|CFB|NoPadding".

## 3DES

The [3DES](./cj-crypto-sym-key-generation-conversion-spec.md#3des) algorithm performs three DES encryption or decryption operations on plaintext/ciphertext data to obtain the corresponding ciphertext or plaintext.

The algorithm library currently provides four common encryption modes for 3DES encryption/decryption: ECB, CBC, OFB, and CFB. Different encryption modes require different encryption/decryption parameters. For details, refer to [ParamsSpec](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#interface-paramsspec).

Since DES is a block cipher algorithm, the block length is 64 bits. In practical applications, the last block of plaintext may be less than 64 bits (8 bytes). In such cases, data padding can be performed using different [padding modes](#padding-modes).

Since padding is required to reach the block size, both PKCS5 and PKCS7 in the actual algorithm library use the block size as the padding length, meaning 3DES encryption pads to 8 bytes.

> **Note:**
>
> For ECB and CBC encryption modes, if the plaintext length is not an integer multiple of 64 bits, padding must be used to complete the block.

Currently, 3DES encryption/decryption can be performed using string parameters. The "string parameter" is constructed by concatenating the "symmetric key type (encryption/decryption algorithm + key length)", "block mode", and "padding mode" with the "|" symbol. This is used to specify the algorithm specification when creating a symmetric encryption/decryption instance.

- As shown in the table below, only one item can be selected from each range (i.e., the content within []) to complete the string concatenation.

  Examples:
  
    - For a 3DES key with ECB block mode, 192-bit key length, and PKCS7 padding mode, the string parameter is "3DES192|ECB|PKCS7".
    - For a 3DES key with OFB block mode, 192-bit key length, and NoPadding mode, the string parameter is "3DES192|OFB|NoPadding".

  | Block Mode | Key Length (bit) | Padding Mode | API Version |
  | :-------- | :-------- | :-------- | :-------- |
  | ECB | 192 | [NoPadding\|PKCS5\|PKCS7] | 12+ |
  | CBC | 192 | [NoPadding\|PKCS5\|PKCS7] | 12+ |
  | OFB | 192 | [NoPadding\|PKCS5\|PKCS7] | 12+ |
  | CFB | 192 | [NoPadding\|PKCS5\|PKCS7] | 12+ |

- Symmetric encryption/decryption without key length specification is supported. When inputting the key type for encryption/decryption parameters, the key length can be omitted, and the encryption/decryption operation will depend on the actual input key length.

  Example: For a 3DES key with CFB block mode, no key length specified, and NoPadding mode, the string parameter is "3DES|CFB|NoPadding".

## SM4

The algorithm library currently provides seven common encryption modes for [SM4](./cj-crypto-sym-key-generation-conversion-spec.md#sm4) encryption/decryption: ECB, CBC, CTR, OFB, CFB, CFB128, and GCM. Different encryption modes require different encryption/decryption parameters. For details, refer to [ParamsSpec](../../../../en/application-dev/reference/CryptoArchitectureKit/cj-apis-crypto.md#interface-paramsspec).

Since SM4 is a block cipher algorithm, the block length is 128 bits. In practical applications, the last block of plaintext may be less than 128 bits (16 bytes). In such cases, data padding can be performed using different [padding modes](#padding-modes).

Since padding is required to reach the block size, both PKCS5 and PKCS7 in the actual algorithm library use the block size as the padding length, meaning SM4 encryption pads to 16 bytes.

> **Note:**
>
> For ECB and CBC encryption modes, if the plaintext length is not an integer multiple of 128 bits, padding must be used to complete the block.

Currently, SM4 encryption/decryption can be performed using string parameters. The "string parameter" is constructed by concatenating the "symmetric key type (encryption/decryption algorithm + key length)", "block mode", and "padding mode" with the "|" symbol. The SM4 algorithm and key length are concatenated with the "_" symbol.

Examples:
  
- For an SM4 key with ECB block mode, 128-bit key length, and PKCS7 padding mode, the string parameter is "SM4_128|ECB|PKCS7".
- For an SM4 key with CFB block mode, 128-bit key length, and NoPadding mode, the string parameter is "SM4_128|CFB|NoPadding".
- For an SM4 key with GCM block mode, 128-bit key length, and NoPadding mode, the string parameter is "SM4_128|GCM|NoPadding".

| Block Mode | Key Length (bit) | Padding Mode | API Version |
| :-------- | :-------- | :-------- | :-------- |
| ECB | 128 | [NoPadding\|PKCS5\|PKCS7] | 12+ |
| CBC | 128 | [NoPadding\|PKCS5\|PKCS7] | 12+ |
| CTR | 128 | [NoPadding\|PKCS5\|PKCS7] | 12+ |
| OFB | 128 | [NoPadding\|PKCS5\|PKCS7] | 12+ |
| CFB | 128 | [NoPadding\|PKCS5\|PKCS7] | 12+ |
| CFB128 | 128 | [NoPadding\|PKCS5\|PKCS7] | 12+ |
| GCM | 128 | [NoPadding\|PKCS5\|PKCS7] | 12+ |

## Padding Modes

Block cipher algorithms have fixed block lengths. In practical applications, the last block of plaintext may not meet the fixed length requirement. In such cases, data padding can be performed using different padding modes. The padding modes include:

- NoPadding: No padding. The input data must match the block length.
- PKCS5: The padding characters consist of a sequence of bytes, each filled with the length of the padding sequence. PKCS5 uses 8-byte padding, meaning data is padded to a multiple of 8 bytes.
- PKCS7: The padding method is the same as PKCS5. However, PKCS7 can pad between 1-255 bytes, while PKCS5 is fixed at 8 bytes.

For modes like CFB, OFB, CTR, GCM, and CCM, which convert block ciphers into stream modes, padding is not required. Therefore, regardless of the specified padding mode, they will be implemented as NoPadding.