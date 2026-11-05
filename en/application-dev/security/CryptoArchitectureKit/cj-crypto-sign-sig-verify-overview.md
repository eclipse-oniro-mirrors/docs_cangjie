# Signature/Verification

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

When you need to determine whether received data has been tampered with or whether the data was sent by the specified entity, signature and verification operations can be used.

The following describes the algorithms currently supported by the system and their corresponding specifications.

## RSA

The algorithm library framework currently provides two RSA signature/verification padding modes:

- [PKCS1](#padding-mode-as-pkcs1): Corresponds to the RSAES-PKCS1-V1_5 mode in RFC3447 specification, equivalent to RSA_PKCS1_PADDING in OpenSSL.

  When using this mode, a digest (md) must be set. The output length of the digest algorithm must be less than the RSA key length. For example, the key byte length of RSA2048 is 256.

- [PSS](#padding-mode-as-pss): Corresponds to the RSASSA-PSS mode in RFC3447 specification, equivalent to RSA_PKCS1_PSS_PADDING in OpenSSL.

  When using this mode, two digests (md and mgf1_md) must be set, and the md digest byte length + saltLen + 2 must be less than or equal to the RSA key length.

  This mode also allows additional configuration of the salt length saltLen, and can be used to retrieve PSS-related parameters. (Unit: byte)

  | PSS Parameter | Description |
  | -------- | -------- |
  | md | Digest algorithm. |
  | mgf | Mask generation algorithm. Currently only MGF1 is supported. |
  | mgf1_md | Digest algorithm used in MGF1. |
  | saltLen | Salt length. (Unit: byte) |
  | trailer_field | Integer used for encoding operations. Only supports 1. |

### Padding Mode as PKCS1

RSA signature/verification is performed using string parameters. The specific "string parameter" is formed by concatenating the "asymmetric key type," "padding mode PKCS1," and "digest" with the "|" symbol, used to specify the asymmetric signature/verification algorithm specification when creating an asymmetric signature/verification instance.

As shown in the table, only one item can be selected from each range (i.e., content within []) to form the string parameter. For example, when an RSA key with asymmetric key type RSA512, padding mode PKCS1, and digest algorithm MD5 is required, the string parameter is "RSA512|PKCS1|MD5".

> **Note:**
>
> When performing RSA signature/verification, the output length of the digest algorithm must be less than the RSA key length. For example, when the RSA key is 512 bits, SHA512 is not supported.

| Asymmetric Key Type | Padding Mode | Digest Algorithm | API Version |
| :-------- | :-------- | :-------- | :-------- |
| RSA512 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384] | 12+ |
| RSA768 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA1024 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA2048 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA3072 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA4096 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA8192 | PKCS1 | [MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| RSA | PKCS1 | Digest algorithm meeting length requirements | 12+ |

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the RSA signature/verification parameter supports omitting the key length. The actual signature/verification operation depends on the actual input key length.

### Padding Mode as PSS

RSA signature/verification is performed using string parameters. The specific "string parameter" is formed by concatenating the "asymmetric key type," "padding mode PSS," "digest," and "mask digest" with the "|" symbol, used to specify the asymmetric signature/verification algorithm specification when creating an asymmetric signature/verification instance.

As shown in the table, only one item can be selected from each range (i.e., content within []) to form the string parameter. For example, when an RSA key with asymmetric key type RSA2048, padding mode PSS, digest algorithm SHA256, and mask digest MGF1_SHA256 is required, the string parameter is "RSA2048|PSS|SHA256|MGF1_SHA256".

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
| RSA | PSS | Digest algorithm meeting length requirements | MGF1_Digest algorithm meeting length requirements | 12+ |

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the RSA signature/verification parameter supports omitting the key length. The actual signature/verification operation depends on the actual input key length.

### Retrieving/Setting PSS Padding Mode Parameters

RSA supports retrieving and setting related parameters when using PSS padding mode. "√" indicates support for retrieving or setting the parameter.

| PSS Parameter | Enum Value | Retrieve | Set |
| -------- | -------- | -------- | -------- |
| md | PSS_MD_NAME_STR | √ | - |
| mgf | PSS_MGF_NAME_STR | √ | - |
| mgf1_md | PSS_MGF1_MD_STR | √ | - |
| saltLen | PSS_SALT_LEN_NUM | √ | √ |
| trailer_field | PSS_TRAILER_FIELD_NUM | √ | - |

### OnlySign/OnlyVerify in PKCS1 Mode

The algorithm library framework currently provides RSA signing without digest computation (sign only) capability, and also supports verification without digest computation.

RSA signing is performed using string parameters. The specific "string parameter" is formed by concatenating the "asymmetric key type," "padding mode," "digest," and "sign mode" or "verify mode" with the "|" symbol, used to specify the asymmetric signature algorithm specification when creating an asymmetric signature instance.

As shown in the table, only one item can be selected from each range (i.e., content within []) to form the string parameter. For example, when an RSA key with asymmetric key type RSA2048, padding mode PKCS1, digest algorithm SHA256, and sign mode OnlySign is required, the string parameter is "RSA2048|PKCS1|SHA256|OnlySign". For verify mode OnlyVerify, the string parameter is "RSA2048|PKCS1|SHA256|OnlyVerify".

> **Note:**
>
> When performing RSA sign-only operations, the data to be signed has length requirements:
>
> 1. PKCS1 padding mode with NoHash (no digest algorithm set): the data must be less than the RSA key byte length - 11 (PKCS1 padding length).
> 2. PKCS1 padding mode with any digest algorithm set: the data to be signed must be the corresponding digest data.
> 3. NoPadding (no padding mode set) with NoHash (no digest algorithm set): the data to be signed must have a length equal to the RSA key byte length, and its value must be less than the RSA modulus.

| Asymmetric Key Type | Padding Mode | Digest Algorithm | Sign/Verify Mode | API Version |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| RSA512 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256] | OnlySign/OnlyVerify | 12+ |
| RSA768 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| RSA1024 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| RSA2048 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| RSA3072 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| RSA4096 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| RSA8192 | PKCS1 | [NoHash\|MD5\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| [RSA512\|RSA768\|RSA1024\|RSA2048\|RSA3072\|RSA4096\|RSA8192\|RSA] | NoPadding | NoHash | OnlySign/OnlyVerify | 12+ |
| RSA | PKCS1 | Digest algorithm meeting length requirements | OnlySign/OnlyVerify | 12+ |

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, RSA sign/verify supports omitting the key length when inputting the key type (i.e., using RSA). In this case, whether the algorithm specification is supported depends on the actual key length passed during sign/verify initialization. For example, when using RSA|PKCS1|SHA384, if the key passed during initialization is RSA512, the specification is not supported because it does not meet the length constraint.

### OnlySign/OnlyVerify in PSS Mode

> **Note:**
>
> The asymmetric key types, digest and mask digest value ranges, and length restriction requirements are consistent with the PSS mode signature/verification specifications above.

The OnlySign/OnlyVerify specification for PSS mode is consistent with the PSS signature/verification specification, with the sign/verify mode appended to the end of the string parameter.

String parameter format: "Asymmetric key type|PSS|Digest|Mask digest|Sign/Verify mode".

For example, when an RSA key with asymmetric key type RSA2048, padding mode PSS, digest algorithm SHA256, mask digest MGF1_SHA256, and sign mode OnlySign is required, the string parameter is "RSA2048|PSS|SHA256|MGF1_SHA256|OnlySign". For verify mode OnlyVerify, the string parameter is "RSA2048|PSS|SHA256|MGF1_SHA256|OnlyVerify".

### Verify Mode as Recover

The algorithm library framework currently provides RSA signature recovery capability to recover the original data from signature data.

RSA signature recovery is performed using string parameters. The specific "string parameter" is formed by concatenating the "asymmetric key type," "padding mode," "digest," and "verify mode" with the "|" symbol, used to specify the asymmetric verification algorithm specification when creating an asymmetric verification instance.

As shown in the table, only one item can be selected from each range (i.e., content within []) to form the string parameter. For example, when an RSA key with asymmetric key type RSA2048, padding mode PKCS1, digest algorithm SHA256, and verify mode Recover is required, the string parameter is "RSA2048|PKCS1|SHA256|Recover".

| Asymmetric Key Type | Padding Mode | Digest Algorithm | Verify Mode | API Version |
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

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the RSA signature recovery parameter supports omitting the key length. The actual signature recovery operation depends on the actual input key length.

## ECDSA

ECDSA (Elliptic Curve Digital Signature Algorithm) is a digital signature algorithm (DSA) based on elliptic curve cryptography (ECC). Compared to DLP (Discrete Logarithm Problem) and IFP (Integer Factorization Problem), elliptic curve cryptography offers higher security strength per bit than other public-key systems.

The algorithm library framework provides ECDSA signature/verification capabilities with various combinations of elliptic curves and digest algorithms, and also supports OnlySign and OnlyVerify modes.

ECDSA signature/verification is performed using string parameters. The specific "string parameter" is formed by concatenating the "asymmetric key type" and "digest" with the "|" symbol, used to specify the asymmetric signature/verification algorithm specification when creating an asymmetric signature/verification instance.

As shown in the table, only one item can be selected from each range (i.e., content within []) to form the string parameter. For example, when an ECC key with asymmetric key type ECC224 and digest algorithm SHA256 is required, the string parameter is "ECC224|SHA256". For OnlySign and OnlyVerify modes, the string parameters are "ECC224|SHA256|OnlySign" and "ECC224|SHA256|OnlyVerify" respectively.

| Asymmetric Key Type | Digest | Sign/Verify Mode | API Version |
| :-------- | :-------- | :-------- | :-------- |
| ECC192 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| ECC224 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| ECC256 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| ECC384 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| ECC521 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| ECC_Secp256k1 | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |
| ECC | [SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | OnlySign/OnlyVerify | 12+ |

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the ECDSA signature/verification parameter supports omitting the key length and curve. The actual signature/verification operation depends on the actual input key.

## DSA

DSA (Digital Signature Algorithm) has its security based on the difficulty of the discrete logarithm problem over a finite field of integers, offering good compatibility and applicability.

DSA signature/verification is performed using string parameters. The specific "string parameter" is formed by concatenating the "asymmetric key type" and "digest" with the "|" symbol, used to specify the asymmetric signature/verification algorithm specification when creating an asymmetric signature/verification instance.

| Asymmetric Key Type | Digest | API Version |
| :-------- | :-------- | :-------- |
| DSA1024 | [NoHash\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| DSA2048 | [NoHash\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| DSA3072 | [NoHash\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |
| DSA | [NoHash\|SHA1\|SHA224\|SHA256\|SHA384\|SHA512] | 12+ |

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the DSA signature/verification parameter supports omitting the key length. The actual signature/verification operation depends on the actual input key length.

> **Note:**
>
> When using the DSA algorithm with the digest algorithm set to NoHash, segmented signing or segmented verification is not supported.

## SM2

The SM2 digital signature algorithm is a signature/verification algorithm based on elliptic curves.

SM2 signature/verification is performed using string parameters. The specific "string parameter" is formed by concatenating the "asymmetric key type" and "digest" with the "|" symbol, used to specify the asymmetric signature/verification algorithm specification when creating an asymmetric signature/verification instance.

Currently, SM2 signing only supports the SM3 digest.

| Asymmetric Key Type | Digest | String Parameter | API Version |
| :-------- | :-------- | :-------- | :-------- |
| SM2_256 | SM3 | SM2_256\|SM3 | 12+ |
| SM2 | SM3 | SM2\|SM3 | 12+ |

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the SM2 signature/verification parameter supports omitting the key length. The actual signature/verification operation depends on the actual input key length.

## Ed25519

Ed25519 is a signature/verification algorithm based on elliptic curves.

Ed25519 signature/verification is performed using string parameters, used to specify the asymmetric signature/verification algorithm specification when creating an asymmetric signature/verification instance.

| Asymmetric Key Type | String Parameter | API Version |
| :-------- | :-------- | :-------- |
| Ed25519 | Ed25519 | 12+ |

## ML-DSA

ML-DSA (Module-Lattice-Based Digital Signature Algorithm) is a post-quantum cryptographic algorithm for digital signatures based on module lattices.

Create an ML-DSA signature/verification instance using string parameters.

| Asymmetric Key Type | String Parameter | API Version |
| :-------- | :-------- | :-------- |
| ML-DSA-44 | ML-DSA-44 | 12+ |
| ML-DSA-65 | ML-DSA-65 | 12+ |
| ML-DSA-87 | ML-DSA-87 | 12+ |
