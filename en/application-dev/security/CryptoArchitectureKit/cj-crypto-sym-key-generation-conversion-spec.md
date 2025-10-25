# Symmetric Key Generation and Conversion Specifications

This section describes the currently supported algorithms and their corresponding specifications in the system.

Developers can generate corresponding keys by using string parameters to carry key specifications. The supported string parameters for each algorithm will be introduced in the specific specifications of each algorithm.

## AES

AES (Advanced Encryption Standard), the most common symmetric encryption algorithm.

Basic characteristics:

- Block cipher algorithm with a block length of 128 bits.
- Key lengths of 128 bits, 192 bits, or 256 bits.
- Compared to 3DES, it offers higher security and faster processing speed.

Currently supports generating AES keys using string parameters. The specific "string parameter" is formed by concatenating the "symmetric key algorithm" and "key length", used to specify the key specification when creating a symmetric key generator.

| Symmetric Key Algorithm | Key Length (bit) | String Parameter | API Version |
| :-------- | :-------- | :-------- | :-------- |
| AES | 128 | AES128 | 12+ |
| AES | 192 | AES192 | 12+ |
| AES | 256 | AES256 | 12+ |

## 3DES

3DES (Triple Data Encryption Algorithm), also known as 3DESede or TripleDES.

Basic characteristics:

- Uses three 64-bit keys to perform triple encryption on data, equivalent to applying the DES (Data Encryption Standard) encryption algorithm three times to each data block.
- Compared to DES, 3DES has longer key lengths and higher security, but slower processing speed than DES.

Currently supports generating 3DES keys using string parameters. The specific "string parameter" is formed by concatenating the "symmetric key algorithm" and "key length", used to specify the key specification when creating a symmetric key generator.

| Symmetric Key Algorithm | Key Length (bit) | String Parameter | API Version |
| :-------- | :-------- | :-------- | :-------- |
| 3DES | 192 | 3DES192 | 12+ |

## SM4

SM4, the SM4 block cipher algorithm.

Basic characteristics:

- Block cipher algorithm with a block length of 128 bits.
- Key length of 128 bits. Can be extended to increase key length.
- Both the encryption algorithm and key expansion algorithm use a 32-round nonlinear iterative structure. The algorithm structures for data decryption and data encryption are identical, except that the order of round keys is reversed—the decryption round keys are the inverse sequence of the encryption round keys.

Currently supports generating SM4 keys using string parameters. The specific "string parameter" is formed by concatenating the "symmetric key algorithm" and "key length" with the connector "_", used to specify the key specification when creating a symmetric key generator.

| Symmetric Key Algorithm | Key Length (bit) | String Parameter | API Version |
| :-------- | :-------- | :-------- | :-------- |
| SM4 | 128 | SM4_128 | 12+ |

## HMAC

HMAC (Hash-based Message Authentication Code), a hash-based message authentication code algorithm that requires a symmetric key as input during computation.

Basic characteristics of HMAC:

- The symmetric key used can be of any length:
  - If the key length exceeds the HMAC block length, the result of a one-way hash of the key is used as the new key.
  - If the key length is less than the HMAC block length, it is padded with zeros at the end to form the new key, ensuring the final key length matches the HMAC block length.
  - The recommended key length is the output length of the digest algorithm.

Currently supports generating symmetric keys for HMAC using string parameters:

- When the HMAC key length matches the output length of the digest algorithm, the specific "string parameter" is formed by concatenating the "message authentication code algorithm" and "digest algorithm" with the connector "|", used to specify the key specification when creating a symmetric key generator.
- When the HMAC key length falls outside the output length range of the above digest algorithms, a symmetric key generator can be created using the string parameter "HMAC", and the key can be generated based on the binary data of the HMAC key.

| Message Authentication Code Algorithm | Digest Algorithm | Key Length (bit) | String Parameter | API Version |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| HMAC | SHA1 | 160 | HMAC\|SHA1 | 12+ |
| HMAC | SHA224 | 224 | HMAC\|SHA224 | 12+ |
| HMAC | SHA256 | 256 | HMAC\|SHA256 | 12+ |
| HMAC | SHA384 | 384 | HMAC\|SHA384 | 12+ |
| HMAC | SHA512 | 512 | HMAC\|SHA512 | 12+ |
| HMAC | SM3 | 256 | HMAC\|SM3 | 12+ |
| HMAC | - | [1, 32768] | HMAC | 12+ |