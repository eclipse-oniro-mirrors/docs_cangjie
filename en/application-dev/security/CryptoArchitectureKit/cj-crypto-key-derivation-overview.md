# Introduction to Key Derivation and Algorithm Specifications

A key derivation function (KDF) refers to a pseudo-random function used to derive one or more cryptographic keys from a secret value. Key derivation functions can be employed to extend keys into longer keys or obtain keys in desired formats.

## PBKDF2 Algorithm

PBKDF (Password-Based Key Derivation Function) is a key derivation function with adjustable computational cost, and PBKDF2 is one of the standards in the PKCS series.

PBKDF2 utilizes a pseudo-random function PRF (Pseudo-Random Function, such as hash-based [HMAC](./cj-crypto-compute-mac.md)), taking a plaintext password and salt value as input, and performs repeated iterations for key derivation.

Currently, string parameters are supported for key derivation. The specific "string parameter" is formed by concatenating the "key derivation function" and "HMAC function digest algorithm" with the "|" symbol, used to specify algorithm specifications when creating a key derivation function generator.

| Key Derivation Algorithm | HMAC Function Digest Algorithm | String Parameter | API Version |
| :---------------------- | :---------------------------- | :---------------- | :---------- |
| PBKDF2 | SHA1 | PBKDF2\|SHA1 | 12+ |
| PBKDF2 | SHA224 | PBKDF2\|SHA224 | 12+ |
| PBKDF2 | SHA256 | PBKDF2\|SHA256 | 12+ |
| PBKDF2 | SHA384 | PBKDF2\|SHA384 | 12+ |
| PBKDF2 | SHA512 | PBKDF2\|SHA512 | 12+ |
| PBKDF2 | SM3 | PBKDF2\|SM3 | 12+ |

## HKDF Algorithm

HKDF (HMAC-based Extract-and-Expand Key Derivation Function) is a simple key derivation function based on [HMAC](./cj-crypto-compute-mac.md) message authentication code. It extracts by inputting original key material and salt value, and expands by inputting original key material and expansion information. It is a key derivation function used to derive longer output keys from shorter input keys.

HKDF includes three modes: extract (EXTRACT_ONLY), expand (EXPAND_ONLY), and extract-and-expand (EXTRACT_AND_EXPAND).

- Extract: Uses original key material to derive a cryptographically strong pseudo-random key.
- Expand: Extends a short key into a longer one, using the extracted pseudo-random key to expand into a key of specified length while maintaining randomness.
- Extract-and-Expand: Derives a pseudo-random key and expands it into a key of specified length.

Currently, string parameters are supported for key derivation. The specific "string parameter" is formed by concatenating the "key derivation function", "HMAC function digest algorithm", and "mode" with the "|" symbol, used to specify algorithm specifications when creating a key derivation function generator.

| Key Derivation Algorithm | HMAC Function Digest Algorithm | Mode | String Parameter | API Version |
| :---------------------- | :---------------------------- | :--- | :---------------- | :---------- |
| HKDF | SHA1 | [EXPAND_ONLY\|EXTRACT_ONLY\|EXTRACT_AND_EXPAND] | HKDF\|SHA1 | 12+ |
| HKDF | SHA224 | [EXPAND_ONLY\|EXTRACT_ONLY\|EXTRACT_AND_EXPAND] | HKDF\|SHA224 | 12+ |
| HKDF | SHA256 | [EXPAND_ONLY\|EXTRACT_ONLY\|EXTRACT_AND_EXPAND] | HKDF\|SHA256 | 12+ |
| HKDF | SHA384 | [EXPAND_ONLY\|EXTRACT_ONLY\|EXTRACT_AND_EXPAND] | HKDF\|SHA384 | 12+ |
| HKDF | SHA512 | [EXPAND_ONLY\|EXTRACT_ONLY\|EXTRACT_AND_EXPAND] | HKDF\|SHA512 | 12+ |
| HKDF | SM3 | [EXPAND_ONLY\|EXTRACT_ONLY\|EXTRACT_AND_EXPAND] | HKDF\|SM3 | 12+ |