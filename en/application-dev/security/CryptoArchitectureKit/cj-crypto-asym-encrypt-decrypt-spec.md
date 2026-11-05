# Asymmetric Key Encryption/Decryption Algorithm Specifications

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This document introduces the asymmetric encryption/decryption algorithms currently supported by Cangjie and their corresponding specifications.

For each algorithm, the supported encryption modes will be described in their respective algorithm specifications.

## RSA

RSA is an asymmetric encryption algorithm that requires fixed-length input for encryption. In practical applications, data may not meet the fixed-length requirement, in which case different padding modes can be used for data padding.

Cangjie currently supports the following three RSA encryption/decryption modes:

- [NoPadding](#padding-mode-as-nopadding): No padding. The input data must be exactly the same length as the RSA key byte length; the output data length equals the RSA key byte length.
- [PKCS1](#padding-mode-as-pkcs1): Corresponds to the RSAES-PKCS1-V1_5 mode in RFC3447 specification, equivalent to RSA_PKCS1_PADDING in OpenSSL.
  During RSA operations, source data D needs to be converted into an Encryption Block (EB). For encryption, the maximum input data length ≤ RSA key byte length - 11; the output data length equals the RSA key byte length.
- [PKCS1_OAEP](#padding-mode-as-pkcs1_oaep): Corresponds to the RSAES-OAEP mode in RFC3447 specification, equivalent to RSA_PKCS1_OAEP_PADDING in OpenSSL.
  This mode requires setting two digests (md and mgf1_md). For encryption, the input data must be less than RSA key byte length - 2 * md digest byte length - 2; the output data length equals the RSA key byte length.

  This mode also allows additional configuration of a pSource byte stream to define the encoding input for OAEP padding, and can retrieve PKCS1_OAEP related parameters (as shown in the table).

  | PKCS1_OAEP Parameters | Description |
  | -------- | -------- |
  | md | Digest algorithm. |
  | mgf | Mask generation algorithm (currently only MGF1 is supported). |
  | mgf1_md | Digest algorithm used in MGF1. |
  | pSource | Byte stream for encoding input. |

Using RSA2048|SHA256 as an example, the relationship between input data length and the algorithm is illustrated below.

| Padding Mode | Maximum Input Data Byte Length | Maximum Output Data Byte Length |
| -------- | -------- | -------- |
| NoPadding | 256 (RSA key byte length) | 256 |
| PKCS1 | 245 (RSA key byte length - 11) | 256 |
| PKCS1_OAEP | 190 (RSA key byte length - 2 * md digest byte length - 2) | 256 |

> **Note:**
>
> Using synchronous interfaces to generate RSA2048, RSA3072, RSA4096, or RSA8192 asymmetric keys, or when the plaintext length exceeds 2048, will result in increased processing time.

### Padding Mode as NoPadding

RSA encryption/decryption is performed using string parameters. The specific "string parameter" is formed by concatenating the "asymmetric key type" and "padding mode NoPadding" with the "|" symbol, used to specify the algorithm specification when creating an asymmetric encryption/decryption instance.

| Asymmetric Key Type | String Parameter | API Version |
| -------- | -------- | -------- |
| RSA512 | RSA512\|NoPadding | 12+ |
| RSA768 | RSA768\|NoPadding | 12+ |
| RSA1024 | RSA1024\|NoPadding | 12+ |
| RSA2048 | RSA2048\|NoPadding | 12+ |
| RSA3072 | RSA3072\|NoPadding | 12+ |
| RSA4096 | RSA4096\|NoPadding | 12+ |
| RSA8192 | RSA8192\|NoPadding | 12+ |
| RSA | RSA\|NoPadding | 12+ |

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the RSA encryption/decryption parameter supports omitting the key length. The actual encryption/decryption operation depends on the input key length.

### Padding Mode as PKCS1

RSA encryption/decryption is performed using string parameters. The specific "string parameter" is formed by concatenating the "asymmetric key type" and "padding mode PKCS1" with the "|" symbol, used to specify the algorithm specification when creating an asymmetric encryption/decryption instance.

| Asymmetric Key Type | String Parameter | API Version |
| -------- | -------- | -------- |
| RSA512 | RSA512\|PKCS1 | 12+ |
| RSA768 | RSA768\|PKCS1 | 12+ |
| RSA1024 | RSA1024\|PKCS1 | 12+ |
| RSA2048 | RSA2048\|PKCS1 | 12+ |
| RSA3072 | RSA3072\|PKCS1 | 12+ |
| RSA4096 | RSA4096\|PKCS1 | 12+ |
| RSA8192 | RSA8192\|PKCS1 | 12+ |
| RSA | RSA\|PKCS1 | 12+ |

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the RSA encryption/decryption parameter supports omitting the key length. The actual encryption/decryption operation depends on the input key length.

### Padding Mode as PKCS1_OAEP

RSA encryption/decryption is performed using string parameters. The specific "string parameter" is formed by concatenating the "asymmetric key type," "padding mode PKCS1_OAEP," digest, and mask digest with the "|" symbol, used to specify the algorithm specification when creating an asymmetric encryption/decryption instance.

As shown in the table, only one item can be selected from each range (i.e., content within []) to form the string parameter.

For example, when an RSA key with asymmetric key type RSA2048, padding mode PKCS1_OAEP, digest algorithm SHA256, and mask digest MGF1_SHA256 is required, the string parameter is "RSA2048|PKCS1_OAEP|SHA256|MGF1_SHA256".

> **Note:**
>
> The input data must be less than RSA key byte length - md digest length - mgf1_md digest length - 2. For example, when the RSA key is 512 bits, SHA512 is not supported.

| Asymmetric Key Type | Padding Mode | Digest | Mask Digest | API Version |
| -------- | -------- | -------- | -------- | -------- |
| RSA512 | PKCS1_OAEP | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256] | 12+ |
| RSA512 | PKCS1_OAEP | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256] | 12+ |
| RSA512 | PKCS1_OAEP | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256] | 12+ |
| RSA768 | PKCS1_OAEP | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA768 | PKCS1_OAEP | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA768 | PKCS1_OAEP | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA768 | PKCS1_OAEP | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384] | 12+ |
| RSA1024 | PKCS1_OAEP | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA1024 | PKCS1_OAEP | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA1024 | PKCS1_OAEP | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA1024 | PKCS1_OAEP | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA1024 | PKCS1_OAEP | SHA384 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA2048 | PKCS1_OAEP | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA2048 | PKCS1_OAEP | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA2048 | PKCS1_OAEP | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA2048 | PKCS1_OAEP | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA2048 | PKCS1_OAEP | SHA384 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA2048 | PKCS1_OAEP | SHA512 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PKCS1_OAEP | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PKCS1_OAEP | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PKCS1_OAEP | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PKCS1_OAEP | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PKCS1_OAEP | SHA384 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PKCS1_OAEP | SHA512 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PKCS1_OAEP | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PKCS1_OAEP | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PKCS1_OAEP | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PKCS1_OAEP | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PKCS1_OAEP | SHA384 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PKCS1_OAEP | SHA512 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PKCS1_OAEP | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PKCS1_OAEP | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PKCS1_OAEP | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PKCS1_OAEP | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PKCS1_OAEP | SHA384 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PKCS1_OAEP | SHA512 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA | PKCS1_OAEP | Digest algorithm meeting length requirements | MGF1_Digest algorithm meeting length requirements | 12+ |

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the RSA encryption/decryption parameter supports omitting the key length. The actual encryption/decryption operation depends on the input key length.

### Retrieving/Setting OAEP Padding Mode Parameters

Starting from API version 12, RSA supports retrieving and setting related parameters when using PKCS1_OAEP padding mode. "√" indicates support for retrieving or setting the parameter.

| OAEP Parameter | Enum Value | Retrieve | Set |
| -------- | -------- | -------- | -------- |
| md | OAEP_MD_NAME_STR | √ | - |
| mgf | OAEP_MGF_NAME_STR | √ | - |
| mgf1_md | OAEP_MGF1_MD_STR | √ | - |
| pSource | OAEP_MGF1_PSRC_UINT8ARR | √ | √ |

## SM2

SM2 is an asymmetric encryption algorithm that requires fixed-length input for encryption. Cangjie currently supports encrypting or decrypting data in the format defined by GM/T 0009-2012.

The result of SM2 asymmetric encryption consists of three parts: C1, C2, and C3. Here, C1 is an elliptic curve point calculated from a generated random number, C2 is the ciphertext data, and C3 is a value computed using a specified digest algorithm.

Currently, SM2 encryption/decryption can be performed using string parameters. The "string parameter" is formed by concatenating the "asymmetric key type (encryption/decryption algorithm + key length)" and "digest algorithm" with the "|" symbol, used to specify the algorithm specification when creating a symmetric encryption/decryption instance.

As shown in the table, only one item can be selected from each range (i.e., content within []) to form the string parameter. The SM2 algorithm and key length are concatenated with the "_" symbol.

For example, when an SM2 key with key length 256 bits and digest algorithm MD5 is required, the string parameter is "SM2_256|MD5".

| Asymmetric Key Type | Digest Algorithm | API Version |
| -------- | -------- | -------- |
| SM2_256 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512\|SM3] | 12+ |
| SM2 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512\|SM3] | 12+ |

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the SM2 encryption/decryption parameter supports omitting the key length. The actual encryption/decryption operation depends on the actual input key length.

### Retrieving SM2 Digest Algorithm Parameters

Starting from API version 12, SM2 supports retrieving digest algorithm parameters. "√" indicates support for retrieving or setting the parameter.

| SM2 Encryption/Decryption Parameter | Enum Value | Retrieve | Set |
| --------  | -------- | -------- | -------- |
| md | SM2_MD_NAME_STR | √ | - |

### Converting SM2 Ciphertext Format

Starting from API version 12, SM2 format conversion is supported. The currently supported SM2 ciphertext format is the ASN.1 format of the national cryptographic standard, where the parameter combination order is C1C3C2.

Developers can specify SM2 ciphertext parameters and convert them into ASN.1 format ciphertext that complies with the national cryptographic standard. Conversely, specific SM2 ciphertext parameters can also be extracted from the ASN.1 format ciphertext of the national cryptographic standard, allowing developers to assemble them into other SM2 ciphertext formats.

SM2 ciphertext parameters include:

- xCoordinate: x component, i.e., C1_X.
- yCoordinate: y component, i.e., C1_Y. xCoordinate and yCoordinate can be converted into C1.
- cipherTextData: Ciphertext, i.e., C2.
- hashData: Hash value, i.e., C3.

Currently, SM2 ciphertext format conversion mode can be specified using string parameters, as shown in the table below. "√" indicates support for generating or retrieving parameters.

| SM2 Ciphertext Format Conversion Mode | Generate SM2 Ciphertext from Parameters | Retrieve Parameters from SM2 Ciphertext |
| --------  | -------- | -------- |
| C1C3C2 | √ | √ |