# Introduction to Key Derivation and Algorithm Specifications

## Introduction to Key Derivation

In cryptography, a Key Derivation Function (KDF) uses a pseudorandom function to derive one or more secret keys from a secret value such as a master password or passphrase.

> **Note:**
>
> * In HUKS, key derivation can only be performed using HUKS-managed keys.
> * Lightweight devices do not support key derivation functionality.
> * Using an existing key alias as the derived result key alias will overwrite the existing key.

## Supported Algorithms

The following are the specifications supported for key derivation.

<!--Del-->
For OpenHarmony, vendor adaptation specifications for key management services are divided into mandatory and optional specifications. Mandatory specifications are algorithm specifications supported by all vendors. For optional specifications, vendors will decide whether to implement them based on actual circumstances. If needed, please refer to the specific vendor's documentation to ensure support before use.

**Developers are advised to use mandatory specifications for application development to ensure full platform compatibility.**
<!--DelEnd-->

Derived keys are session key results obtained by services through a three-stage process. Services can decide whether the derived keys are managed by HUKS (i.e., keys do not leave the [TEE](./cj-huks-concepts.md)) or managed independently by the service.

> **Note:**
>
> PBKDF2/HKDF only supports derivation from HUKS-managed keys and does not support direct derivation from non-HUKS-managed keys, such as user passwords. For key hosting, refer to [Key Import](./cj-huks-key-import-overview.md).

| Algorithm/Digest | Derived Key Algorithm/Length | Derived Result Key Usable Algorithms/Length | API Level | <!--DelCol5-->Mandatory Specification |
| :-------- | :-------- | :-------- | :-------- |
| HKDF/SHA256 | AES/192-256 | AES/128/192/256<br/>HMAC/8-1024<br/>SM4/128 | 15+ | Yes |
| HKDF/SHA384 | AES/256 | AES/128/192/256<br/>HMAC/8-1024<br/>SM4/128 | 15+ | Yes |
| HKDF/SHA512 | AES/256 | AES/128/192/256<br/>HMAC/8-1024<br/>SM4/128 | 15+ | Yes |
| PBKDF2/SHA256 | AES/192-256 | AES/128/192/256<br/>HMAC/8-1024<br/>SM4/128 | 15+ | Yes |
| PBKDF2/SHA384 | AES/256 | AES/128/192/256<br/>HMAC/8-1024<br/>SM4/128 | 15+ | Yes |
| PBKDF2/SHA512 | AES/256 | AES/128/192/256<br/>HMAC/8-1024<br/>SM4/128 | 15+ | Yes |
<!--RP1--><!--RP1End-->