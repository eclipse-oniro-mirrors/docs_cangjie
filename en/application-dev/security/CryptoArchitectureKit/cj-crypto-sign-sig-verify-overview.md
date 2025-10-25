# Signature Generation and Verification Introduction and Algorithm Specifications

When it is necessary to determine whether received data has been tampered with or whether the data was sent by a specified entity, signature generation and verification operations can be used.

The following sections describe the algorithms currently supported by the system and their corresponding specifications.

## RSA

The algorithm library framework currently provides two RSA signature padding modes:

- [PKCS1](#padding-mode-as-pkcs1): Corresponds to the RSAES-PKCS1-V1_5 mode in RFC3447, equivalent to RSA_PKCS1_PADDING in OpenSSL.

  When using this mode, a digest (md) must be set, and the output length of the digest algorithm must be less than the RSA key length. For example, an RSA2048 key has a bit length of 2048 bits (256 bytes).

- [PSS](#padding-mode-as-pss): Corresponds to the RSASSA-PSS mode in RFC3447, equivalent to RSA_PKCS1_PSS_PADDING in OpenSSL.

  When using this mode, two digests (md and mgf1_md) must be set, and the combined length of md and mgf1_md must be less than the RSA key length. For example, an RSA2048 key has a bit length of 2048 bits (256 bytes).

  This mode also allows additional configuration of the salt length (saltLen) for obtaining PSS-related parameters. (Unit: bytes)

  | PSS Parameters | Description |
  | :-------- | :-------- |
  | md | Digest algorithm. |
  | mgf | Mask generation algorithm; currently only MGF1 is supported. |
  | mgf1_md | Digest algorithm used in the MGF1 algorithm. |
  | saltLen | Salt length. (Unit: bytes) |
  | trailer_field | Integer used for encoding operations; only supports the value 1. |

> **Note:**
>
> Using synchronous interfaces to generate RSA2048, RSA3072, RSA4096, or RSA8192 asymmetric keys or plaintext exceeding 2048 bytes will result in increased processing time.

### Padding Mode as PKCS1

RSA signature generation and verification are completed using string parameters. The specific "string parameter" is constructed by concatenating "asymmetric key type," "padding mode PKCS1," and "digest algorithm" with the "|" symbol. This is used to specify the asymmetric signature algorithm specifications when creating an asymmetric signature instance.

As shown in the table, only one option can be selected from each range (i.e., the content within `[]`) to form the string. For example, when an asymmetric key of type RSA512, padding mode PKCS1, and digest algorithm MD5 is required, the string parameter is "RSA512|PKCS1|MD5".

> **Note:**
>
> For RSA signature generation and verification, the output length of the digest algorithm must be less than the RSA key length. For example, an RSA key of 512 bits does not support SHA512.

| Asymmetric Key Type | Padding Mode | Digest Algorithm | API Version |
| :-------- | :-------- | :-------- | :-------- |
| RSA512 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256] | 12+ |
| RSA768 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA1024 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA2048 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA3072 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA4096 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA8192 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA | PKCS1 | Digest algorithm meeting length requirements | 12+ |

As shown in the last row of the table, to ensure compatibility with keys generated from key parameters, the RSA signature parameter supports omitting the key length when inputting the key type. The signature operation depends on the actual input key length.

### Padding Mode as PSS

RSA signature generation and verification are completed using string parameters. The specific "string parameter" is constructed by concatenating "asymmetric key type," "padding mode PSS," "digest algorithm," and "mask digest algorithm" with the "|" symbol. This is used to specify the asymmetric signature algorithm specifications when creating an asymmetric signature instance.

As shown in the table, only one option can be selected from each range (i.e., the content within `[]`) to form the string. For example, when an asymmetric key of type RSA2048, padding mode PSS, digest algorithm SHA256, and mask digest MGF1_SHA256 is required, the string parameter is "RSA2048|PSS|SHA256|MGF1_SHA256".

> **Note:**
>
> For RSA signature generation and verification in PSS mode, the combined length of md and mgf1_md must be less than the RSA key length. For example, an RSA key of 512 bits cannot support both md and mgf1_md being SHA256.

| Asymmetric Key Type | Padding Mode | Digest | Mask Digest | API Version |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| RSA512 | PSS | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256] | 12+ |
| RSA512 | PSS | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256] | 12+ |
| RSA512 | PSS | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256] | 12+ |
| RSA512 | PSS | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224] | 12+ |
| RSA768 | PSS | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA768 | PSS | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA768 | PSS | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA768 | PSS | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384] | 12+ |
| RSA768 | PSS | SHA384 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256] | 12+ |
| RSA768 | PSS | SHA512 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224] | 12+ |
| RSA1024 | PSS | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA1024 | PSS | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA1024 | PSS | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA1024 | PSS | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA1024 | PSS | SHA384 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA1024 | PSS | SHA512 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384] | 12+ |
| RSA2048 | PSS | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA2048 | PSS | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA2048 | PSS | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA2048 | PSS | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA2048 | PSS | SHA384 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA2048 | PSS | SHA512 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PSS | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PSS | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PSS | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PSS | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PSS | SHA384 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA3072 | PSS | SHA512 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PSS | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PSS | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PSS | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PSS | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PSS | SHA384 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA4096 | PSS | SHA512 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PSS | MD5 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PSS | SHA1 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PSS | SHA224 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PSS | SHA256 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PSS | SHA384 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA8192 | PSS | SHA512 | [MGF1_MD5\|MGF1_SHA1\|MGF1_SHA224\|MGF1_SHA256\|MGF1_SHA384\|MGF1_SHA512] | 12+ |
| RSA | PSS | Digest Algorithm Meeting Length Requirements | MGF1_Digest Algorithm Meeting Length Requirements | 12+ |

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the RSA signature verification parameters support inputting key types without specifying length when accepting key inputs. The actual signature verification operation depends on the length of the input key.

### Obtaining/Setting PSS Padding Mode Parameters

Currently supports obtaining and setting related parameters when RSA uses PSS padding mode. "√" indicates support for obtaining or setting the parameter.

| PSS Parameter | Enum Value | Get | Set |
| :-------- | :-------- | :-------- | :-------- |
| md | PSS_MD_NAME_STR | √ | - |
| mgf | PSS_MGF_NAME_STR | √ | - |
| mgf1_md | PSS_MGF1_MD_STR | √ | - |
| saltLen | PSS_SALT_LEN_NUM | √ | √ |
| trailer_field | PSS_TRAILER_FIELD_NUM | √ | - |

### Signature Mode as OnlySign

The algorithm library framework currently provides RSA signature functionality without digest (OnlySign).

RSA signature is completed using string parameters. The specific "string parameter" is constructed by concatenating "asymmetric key type," "padding mode," "digest algorithm," and "signature mode" with the "|" symbol. This is used to specify the asymmetric signature algorithm specifications when creating an asymmetric signature instance.

As shown in the table, only one option can be selected from each range (i.e., the content within `[]`) to form the string. For example, when an asymmetric key of type RSA2048, padding mode PKCS1, digest algorithm SHA256, and signature mode OnlySign is required, the string parameter is "RSA2048|PKCS1|SHA256|OnlySign".

> **Note:**
>
> - For RSA signature without digest, there are length requirements for the data to be signed:
>   - PKCS1 padding mode with NoHash (no digest algorithm): Data must be less than RSA key byte length minus 11 (PKCS1 padding length).
>   - PKCS1 padding mode with any digest algorithm: The data to be signed must be the corresponding digest data.
>   - NoPadding mode with NoHash: The data to be signed must equal the RSA key byte length and its value must be less than the RSA modulus.

| Asymmetric Key Type | Padding Mode | Digest Algorithm | Signature Mode | API Version |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| RSA512 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256] | OnlySign | 12+ |
| RSA768 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign | 12+ |
| RSA1024 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign | 12+ |
| RSA2048 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign | 12+ |
| RSA3072 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign | 12+ |
| RSA4096 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign | 12+ |
| RSA8192 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign | 12+ |
| [RSA512\|RSA768\|RSA1024\|RSA2048\|RSA3072\|RSA4096\|RSA8192\|RSA] | NoPadding | NoHash | OnlySign | 12+ |
| RSA | PKCS1 | Digest algorithm meeting length requirements | OnlySign | 12+ |

As shown in the last row of the table, to ensure compatibility with keys generated from key parameters, the RSA signature parameter supports inputting key types without specifying length. The signature operation depends on the actual input key length.

### Verification Mode: Recover

The cryptographic algorithm framework currently provides RSA signature recovery functionality for original data.

To perform RSA signature recovery using string parameters, the specific "string parameter" is constructed by concatenating "asymmetric key type", "padding mode", "digest algorithm", and "verification mode" with the "|" symbol. This is used to specify asymmetric verification algorithm specifications when creating an asymmetric verification instance.

As shown in the table, only one option can be selected from each value range (i.e., content within []) to complete the string concatenation. For example, when an asymmetric key type of RSA2048, padding mode of PKCS1, digest algorithm of SHA256, and verification mode of Recover are required, the string parameter would be "RSA2048|PKCS1|SHA256|Recover".

| Asymmetric Key Type | Padding Mode | Digest Algorithm | Signature Mode | API Version |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| RSA512 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256] | Recover | 12+ |
| RSA768 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | Recover | 12+ |
| RSA1024 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | Recover | 12+ |
| RSA2048 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | Recover | 12+ |
| RSA3072 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | Recover | 12+ |
| RSA4096 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | Recover | 12+ |
| RSA8192 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | Recover | 12+ |
| [RSA512\|RSA768\|RSA1024\|RSA2048\|RSA3072\|RSA4096\|RSA8192\|RSA] | NoPadding | NoHash | Recover | 12+ |
| RSA | PKCS1 | Digest algorithm meeting length requirements | Recover | 12+ |

As shown in the last row of the table, to ensure compatibility with keys generated from key parameters, the RSA signature recovery parameter supports inputting key types without specifying length. The signature recovery operation depends on the actual input key length.

## ECDSA

ECDSA (Elliptic Curve Digital Signature Algorithm) is a digital signature algorithm based on Elliptic Curve Cryptography (ECC). Compared to DLP (Discrete Logarithm Problem) and IFP (Integer Factorization Problem), elliptic curve cryptography offers higher bit strength per unit than other public key systems.

The cryptographic algorithm framework provides ECDSA signature verification capabilities with various combinations of elliptic curves and digest algorithms.

To perform ECDSA signature verification using string parameters, the specific "string parameter" is constructed by concatenating "asymmetric key type" and "digest algorithm" with the "|" symbol. This is used to specify asymmetric signature verification algorithm specifications when creating an asymmetric signature verification instance.

As shown in the table, only one option can be selected from each value range (i.e., content within []) to complete the string concatenation. For example, when an asymmetric key type of ECC224 and digest algorithm of SHA256 are required, the string parameter would be "ECC224|SHA256".

| Asymmetric Key Type | Digest | API Version |
| :-------- | :-------- | :-------- |
| ECC224 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC256 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC384 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC521 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP160r1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP160t1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP192r1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP192t1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP224r1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP224t1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP256r1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP256t1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP320r1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP320t1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP384r1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP384t1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP512r1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_BrainPoolP512t1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC_Secp256k1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| ECC | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |

As shown in the last row of the table, to ensure compatibility with keys generated from key parameters, the ECDSA signature verification parameter supports inputting key types without specifying length or curve. The signature verification operation depends on the actual input key.

## DSA

DSA (Digital Signature Algorithm) derives its security from the difficulty of the discrete logarithm problem in finite fields of integers, offering good compatibility and applicability.

To perform DSA signature verification using string parameters, the specific "string parameter" is constructed by concatenating "asymmetric key type" and "digest algorithm" with the "|" symbol. This is used to specify asymmetric signature verification algorithm specifications when creating an asymmetric signature verification instance.

As shown in the table, only one option can be selected from each value range (i.e., content within []) to complete the string concatenation. For example, when an asymmetric key type of DSA1024 and digest algorithm of SHA256 are required, the string parameter would be "DSA1024|SHA256".

| Asymmetric Key Type | Digest | API Version |
| :-------- | :-------- | :-------- |
| DSA1024 | [NoHash\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| DSA2048 | [NoHash\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| DSA3072 | [NoHash\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| DSA | [NoHash\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |

As shown in the last row of the table, to ensure compatibility with keys generated from key parameters, the DSA signature verification parameter supports inputting key types without specifying length. The signature verification operation depends on the actual input key length.

> **Note:**
>
> When using the DSA algorithm with the digest algorithm set to NoHash, segmented signing or verification is not supported.

## SM2

The SM2 digital signature algorithm is a signature verification algorithm based on elliptic curves.

To perform SM2 signature verification using string parameters, the specific "string parameter" is constructed by concatenating "asymmetric key type" and "digest algorithm" with the "|" symbol. This is used to specify asymmetric signature verification algorithm specifications when creating an asymmetric signature verification instance.

Currently, SM2 signatures only support the SM3 digest.

| Asymmetric Key Type | Digest | String Parameter | API Version |
| :-------- | :-------- | :-------- | :-------- |
| SM2_256 | SM3 | SM2_256\|SM3 | 12+ |
| SM2 | SM3 | SM2\|SM3 | 12+ |

As shown in the last row of the table, to ensure compatibility with keys generated from key parameters, the SM2 signature verification parameter supports inputting key types without specifying length. The signature verification operation depends on the actual input key length.

## Ed25519

Ed25519 is a signature verification algorithm based on elliptic curves.

To perform Ed25519 signature verification using string parameters, the specific "string parameter" is constructed by concatenating "asymmetric key type" with the "|" symbol. This is used to specify asymmetric signature verification algorithm specifications when creating an asymmetric signature verification instance.

| Asymmetric Key Type | String Parameter | API Version |
| :-------- | :-------- | :-------- |
| Ed25519 | Ed25519 | 12+ |
