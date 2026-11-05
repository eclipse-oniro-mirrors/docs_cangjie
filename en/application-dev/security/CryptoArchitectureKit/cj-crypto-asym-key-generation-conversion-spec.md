# Asymmetric Key Generation and Conversion Specifications

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This section describes the algorithms currently supported by the system and their corresponding specifications.

There are two ways to specify key generation specifications:

- String parameter: Describes the key specification to be generated in the form of a string.

- Key parameter: Uses detailed cryptographic information of the key to construct a key object.

Which method is used for each algorithm will be introduced in the specific algorithm specifications.

## RSA

RSA (Rivest–Shamir–Adleman). Currently, both string parameters and key parameters are supported to generate RSA keys.

**Generating with String Parameters**

To generate RSA keys using string parameters, the specific "string parameter" is formed by concatenating the "RSA key type" and "number of primes" with the "|" symbol, used to specify the key specification when creating an asymmetric key generator.

> **Note:**
>
> When generating RSA asymmetric keys, the default number of primes is 2, and the PRIMES_2 parameter can be omitted.

| RSA Key Type | Number of Primes | String Parameter | API Version |
| :-------- | :-------- | :-------- | :-------- |
| RSA512 | 2 | RSA512\|PRIMES_2 | 12+ |
| RSA768 | 2 | RSA768\|PRIMES_2 | 12+ |
| RSA1024 | 2 | RSA1024\|PRIMES_2 | 12+ |
| RSA1024 | 3 | RSA1024\|PRIMES_3 | 12+ |
| RSA2048 | 2 | RSA2048\|PRIMES_2 | 12+ |
| RSA2048 | 3 | RSA2048\|PRIMES_3 | 12+ |
| RSA3072 | 2 | RSA3072\|PRIMES_2 | 12+ |
| RSA3072 | 3 | RSA3072\|PRIMES_3 | 12+ |
| RSA4096 | 2 | RSA4096\|PRIMES_2 | 12+ |
| RSA4096 | 3 | RSA4096\|PRIMES_3 | 12+ |
| RSA4096 | 4 | RSA4096\|PRIMES_4 | 12+ |
| RSA8192 | 2 | RSA8192\|PRIMES_2 | 12+ |
| RSA8192 | 3 | RSA8192\|PRIMES_3 | 12+ |
| RSA8192 | 4 | RSA8192\|PRIMES_4 | 12+ |
| RSA8192 | 5 | RSA8192\|PRIMES_5 | 12+ |

> **Note:**
>
> When creating an RSA asymmetric key generator for random key generation, the generated RSA key specification is consistent with the key specification specified at creation. For key conversion, the generated RSA key specification is consistent with the key data specification specified during conversion.

**Generating with Key Parameters**

RSA key parameters involve three integers, including:

- n: Modulus, a common parameter for both private and public keys.

- sk: privateExponent, commonly written as d in formulas.

- pk: publicExponent, commonly written as e in formulas.

When creating an asymmetric key generator, RSA keys can be generated based on specified public and private key parameters. For details, see the table below:

- √: Indicates that the specific attribute in this column must be specified to constitute the key parameter.

- ×: Indicates that the specific attribute in this column corresponds to a certain key parameter, but generating keys from that key parameter is not currently supported.

| Parameter Name | Common Parameter | Public Key Parameter | Private Key Parameter | Key Pair Parameter |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| n | × | √ | × | √ |
| pk | N/A | √ | N/A | √ |
| sk | N/A | N/A | × | √ |

Based on the table above:

- RSA does not support generating keys by specifying only the common parameter (n).

- RSA does not support generating private keys by specifying the private key parameter (n, sk).

## ECC

ECC (Elliptic Curve Cryptography) is a public-key cryptographic algorithm based on elliptic curve mathematics.

The elliptic curve algorithm can be viewed as arithmetic operations defined over a special set. The ECC keys currently supported by the algorithm library are all elliptic curves over the Fp field, where p is a prime. The Fp field is also called a prime field.

Both string parameters and key parameters are supported to generate ECC keys. Generating common key parameters from curve names is also supported.

**Generating with String Parameters**

To generate ECC keys using string parameters, the specific "string parameter" is formed by concatenating the "asymmetric key algorithm" and "key length," used to specify the key specification when creating an asymmetric key generator.

| Asymmetric Key Algorithm | Key Length (bit) | Curve Name | String Parameter | API Version |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| ECC | 192 | NID_X9_62_prime192v1 | ECC192 | 12+ |
| ECC | 224 | NID_secp224r1 | ECC224 | 12+ |
| ECC | 256 | NID_X9_62_prime256v1 | ECC256 | 12+ |
| ECC | 384 | NID_secp384r1 | ECC384 | 12+ |
| ECC | 521 | NID_secp521r1 | ECC521 | 12+ |
| ECC | 256 | NID_secp256k1 | ECC_Secp256k1 | 12+ |

> **Note:**
>
> When creating an ECC asymmetric key generator for random key generation, the generated ECC key specification is consistent with the key specification specified at creation. For key conversion, the generated ECC key specification is consistent with the key data specification specified during conversion.

**Generating with Key Parameters**

ECC key parameters in the Fp field include:

- p: Prime, used to determine Fp.

- a, b: Determine the equation of the elliptic curve.

- g: A base point on the elliptic curve, represented by gx and gy.

- n: The order of the base point g.

- h: Cofactor.

- sk: Private key, a random integer less than n.

- pk: Public key, a point on the elliptic curve, pk = sk \* g.

When creating an asymmetric key generator, ECC keys can be generated based on specified public and private key parameters. For details, see the table below:

- √: Indicates that the specific attribute in this column must be specified to constitute the key parameter.

| Parameter Name | Common Parameter | Public Key Parameter | Private Key Parameter | Key Pair Parameter |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| fieldType | √ | √ | √ | √ |
| p | √ | √ | √ | √ |
| a | √ | √ | √ | √ |
| b | √ | √ | √ | √ |
| g | √ | √ | √ | √ |
| n | √ | √ | √ | √ |
| h | √ | √ | √ | √ |
| pk | N/A | √ | N/A | √ |
| sk | N/A | N/A | √ | √ |

> **Note:**
>
> - Currently, ECC only supports the Fp field, so fieldType is fixed to "Fp". fieldType and p constitute the field attribute, and currently only ECFieldFp is supported for field.
>
> - g and pk are points on the ECC curve, of type Point, requiring specific X and Y coordinates to be specified.

**Generating Key Parameters from Curve Names**

Generating ECC common key parameters from curve names is supported.

> **Note:**
>
> - The curve name is a required input string parameter. Supported curve names can be found in the "Curve Name" column of the ECC key string parameter table.
>
> - The generated common key parameters can be directly used to randomly generate key pairs, or to construct public key, private key, and key pair parameters.

## DSA

DSA (Digital Signature Algorithm) is a public-key cryptographic algorithm based on modular arithmetic and the discrete logarithm problem over a finite field of integers. It is commonly used for digital signatures and verification, and cannot be used for encryption and decryption.

Currently, both string parameters and key parameters are supported to generate DSA keys.

**Generating with String Parameters**

To generate DSA keys using string parameters, the specific "string parameter" is formed by concatenating the "asymmetric key algorithm" and "key length," used to specify the key specification when creating an asymmetric key generator.

| Asymmetric Key Algorithm | Key Length (bit) | String Parameter | API Version |
| :-------- | :-------- | :-------- | :-------- |
| DSA | 1024 | DSA1024 | 12+ |
| DSA | 2048 | DSA2048 | 12+ |
| DSA | 3072 | DSA3072 | 12+ |

> **Note:**
>
> When the created DSA asymmetric key generator is used for random key generation, the generated key specification is consistent with the key specification specified at creation. For key conversion, the generated key specification is consistent with the key data specification specified during conversion.

**Generating with Key Parameters**

DSA key parameters include:

- p: A prime modulus, with a bit length that is a multiple of 64.

- q: A prime factor of p-1, with a length related to the length of p.

- g: g = (h ^ ((p - 1) / q)) mod p, where h is any integer satisfying 1 &lt; h &lt; p - 1.

- sk: Private key, a randomly generated integer satisfying 0 &lt; sk &lt; q.

- pk: Public key, pk = (g ^ sk) mod p.

When creating an asymmetric key generator, DSA keys can be generated based on specified public and private key parameters. For details, see the table below:

- √: Indicates that the specific attribute in this column must be specified to constitute the key parameter.

- ×: Indicates that the specific attribute in this column corresponds to a certain key parameter, but generating keys from that key parameter is not currently supported.

| Parameter Name | Common Parameter | Public Key Parameter | Private Key Parameter | Key Pair Parameter |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| p | √ | √ | × | √ |
| q | √ | √ | × | √ |
| g | √ | √ | × | √ |
| pk | N/A | √ | N/A | √ |
| sk | N/A | N/A | × | √ |

> **Note:**
>
> - DSA does not support generating private keys by specifying the private key parameter (p, q, g, sk).
>
> - When using common parameters (p, q, g) to generate DSA key pairs, the DSA key length must be at least 1024 bits.

## SM2

SM2 is a public-key cryptographic algorithm based on elliptic curves, using elliptic curves over the Fp field.

Currently, both string parameters and key parameters are supported to generate SM2 keys. Generating common key parameters from curve names is also supported.

**Generating with String Parameters**

Currently, SM2 keys can be generated using string parameters. The specific "string parameter" is formed by concatenating the "asymmetric key algorithm" and "key length" with the "_" symbol, used to specify the key specification when creating an asymmetric key generator.

| Asymmetric Key Algorithm | Key Length (bit) | Curve Name | String Parameter | API Version |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| SM2 | 256 | NID_sm2 | SM2_256 | 12+ |

**Generating with Key Parameters**

SM2 key parameters in the Fp field include:

- p: Prime, used to determine Fp.

- a, b: Determine the equation of the elliptic curve.

- g: A base point on the elliptic curve, represented by gx and gy.

- n: The order of the base point g.

- h: Cofactor.

- sk: Private key, a random integer less than n.

- pk: Public key, a point on the elliptic curve, pk = sk \* g.

When creating an asymmetric key generator, SM2 keys can be generated based on specified public and private key parameters. For details, see the table below:

- √: Indicates that the specific attribute in this column must be specified to constitute the key parameter.

| Parameter Name | Common Parameter | Public Key Parameter | Private Key Parameter | Key Pair Parameter |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| fieldType | √ | √ | √ | √ |
| p | √ | √ | √ | √ |
| a | √ | √ | √ | √ |
| b | √ | √ | √ | √ |
| g | √ | √ | √ | √ |
| n | √ | √ | √ | √ |
| h | √ | √ | √ | √ |
| pk | N/A | √ | N/A | √ |
| sk | N/A | N/A | √ | √ |

> **Note:**
>
> - Currently, SM2 only supports the Fp field, so fieldType is fixed to "Fp". fieldType and p constitute the field attribute, and currently only ECFieldFp is supported for field.
>
> - g and pk are points on the SM2 curve, of type Point, requiring specific X and Y coordinates to be specified.

**Generating Key Parameters from Curve Names**

Generating SM2 common key parameters from curve names is supported.

> **Note:**
>
> - The curve name is a required input string parameter. The supported curve name is "NID_sm2".
>
> - The generated common key parameters can be directly used to randomly generate key pairs, or to construct public key, private key, and key pair parameters.

## Ed25519

The Ed25519 algorithm is a digital signature algorithm based on the EdDSA algorithm, with a key length of 256 bits, implemented using Edwards curves. This algorithm does not support encryption and decryption, and is primarily used for digital signatures and verification.

Currently, both string parameters and key parameters are supported to generate Ed25519 keys.

**Generating with String Parameters**

Generate Ed25519 keys using string parameters to specify the key specification when creating an asymmetric key generator.

| Asymmetric Key Algorithm | String Parameter | API Version |
| :-------- | :-------- | :-------- |
| Ed25519 | Ed25519 | 12+ |

**Generating with Key Parameters**

Ed25519 key parameters include:

- sk: Private key, a 32-byte random value.

- pk: Public key, a 32-byte value derived from the private key.

When creating an asymmetric key generator, Ed25519 keys can be generated based on specified public and private key parameters. For details, see the table below:

- √: Indicates that the specific attribute in this column must be specified to constitute the key parameter.

| Parameter Name | Public Key Parameter | Private Key Parameter | Key Pair Parameter |
| :-------- | :-------- | :-------- | :-------- |
| pk | √ | N/A | √ |
| sk | N/A | √ | √ |

> **Note:**
>
> Ed25519 key parameters do not have common parameters, and generating keys from common parameters is not supported.

## X25519

The X25519 algorithm is a Diffie-Hellman key exchange algorithm used for key agreement.

Both string parameters and key parameters are supported to generate X25519 keys.

**Generating with String Parameters**

Generate X25519 keys using string parameters to specify the key specification.

| Asymmetric Key Algorithm | String Parameter | API Version |
| :-------- | :-------- | :-------- |
| X25519 | X25519 | 12+ |

**Generating with Key Parameters**

X25519 key parameters include:

- sk: Private key, a 32-byte random value.

- pk: Public key, a 32-byte value derived from the private key.

When creating an asymmetric key generator, the support for generating X25519 keys by specifying public/private key parameters is shown in the table below.

- √: Indicates that the specific attribute in this column must be specified to constitute the key parameter.

| Parameter Name | Public Key Parameter | Private Key Parameter | Key Pair Parameter |
| :-------- | :-------- | :-------- | :-------- |
| pk | √ | N/A | √ |
| sk | N/A | √ | √ |

> **Note:**
>
> X25519 does not have common key parameters, and generating keys from common parameters is not supported.

## DH

DH (Diffie–Hellman key exchange) is a key agreement algorithm that only involves the exchange of public keys. It can provide forward secrecy—even if the communication channel is monitored, the private keys of both parties will not be exposed.

Both string parameters and key parameters are supported to generate DH keys. Generating common key parameters from prime length and private key length is also supported.

**Generating with String Parameters**

To generate DH keys using string parameters, the specific "string parameter" is formed by concatenating the "asymmetric key algorithm" and "well-known safe prime group parameter" with the "_" symbol, used to specify the key specification when creating an asymmetric key generator.

| Asymmetric Key Algorithm | Well-Known Safe Prime Group Parameter | Key Length (bit) | String Parameter | API Version |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| DH | MODP_1536 | 1536 | DH_modp1536 | 12+ |
| DH | MODP_2048 | 2048 | DH_modp2048 | 12+ |
| DH | MODP_3072 | 3072 | DH_modp3072 | 12+ |
| DH | MODP_3526 | 3526 | DH_modp3526 | 12+ |
| DH | MODP_4096 | 4096 | DH_modp4096 | 12+ |
| DH | MODP_6144 | 6144 | DH_modp6144 | 12+ |
| DH | MODP_8192 | 8192 | DH_modp8192 | 12+ |
| DH | FFDHE_2048 | 2048 | DH_ffdhe2048 | 12+ |
| DH | FFDHE_3072 | 3072 | DH_ffdhe3072 | 12+ |
| DH | FFDHE_4096 | 4096 | DH_ffdhe4096 | 12+ |
| DH | FFDHE_6144 | 6144 | DH_ffdhe6144 | 12+ |
| DH | FFDHE_8192 | 8192 | DH_ffdhe8192 | 12+ |

**Generating with Key Parameters**

DH key parameters include:

- p: A prime.

- sk: Private key, a random integer.

- pk: Public key, pk = (g ^ sk) mod p, where g is the base point of DH.

When creating an asymmetric key generator, DH keys can be generated based on specified public and private key parameters. For details, see the table below:

- √: Indicates that the specific attribute in this column must be specified to constitute the key parameter.

| Parameter Name | Common Parameter | Public Key Parameter | Private Key Parameter | Key Pair Parameter |
| :-------- | :-------- | :-------- | :-------- | :-------- |
| p | √ | √ | √ | √ |
| pk | N/A | √ | N/A | √ |
| sk | N/A | N/A | √ | √ |

> **Note:**
>
> When using the common parameter (p) to generate a DH key pair, the system automatically uses the base point g from the corresponding well-known safe prime group parameter.

## ML-KEM

ML-KEM (Module-Lattice-Based Key Encapsulation Mechanism) is a post-quantum cryptographic algorithm for key encapsulation based on module lattices.

**Generating with String Parameters**

Generate ML-KEM keys using string parameters to specify the key specification when creating an asymmetric key generator.

| Asymmetric Key Algorithm | String Parameter | API Version |
| :-------- | :-------- | :-------- |
| ML-KEM-512 | ML-KEM-512 | 12+ |
| ML-KEM-768 | ML-KEM-768 | 12+ |
| ML-KEM-1024 | ML-KEM-1024 | 12+ |

## ML-DSA

ML-DSA (Module-Lattice-Based Digital Signature Algorithm) is a post-quantum cryptographic algorithm for digital signatures based on module lattices.

**Generating with String Parameters**

Generate ML-DSA keys using string parameters to specify the key specification when creating an asymmetric key generator.

| Asymmetric Key Algorithm | String Parameter | API Version |
| :-------- | :-------- | :-------- |
| ML-DSA-44 | ML-DSA-44 | 12+ |
| ML-DSA-65 | ML-DSA-65 | 12+ |
| ML-DSA-87 | ML-DSA-87 | 12+ |
