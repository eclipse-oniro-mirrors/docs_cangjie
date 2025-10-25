# Key Usage Introduction and General Process

## Key Usage Introduction

To achieve protection of data confidentiality, integrity, etc., generated/imported keys can be used to perform key operations on data, such as:

- [Encryption and Decryption](./cj-huks-encryption-decryption-overview.md)

- [Signing and Signature Verification](./cj-huks-signing-signature-verification-overview.md)

- [Key Agreement](./cj-huks-key-agreement-overview.md)

- [Key Derivation](./cj-huks-key-derivation-overview.md)

This section provides examples of the above common key operations. These examples do not include secondary identity access control. If key access control is configured, please refer to the usage in [Key Access Control](./cj-huks-identity-authentication-overview.md).

## General Development Process

HUKS operates on data based on key sessions. The following process should be followed when using keys:

1. **(Mandatory)** Initialize a key session [huks.initSession()](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-initsessionstring-huksoptions)

    Pass in the key alias and key operation parameters to initialize a key session and obtain a session handle. The key operation parameters must include the necessary parameters for the corresponding cryptographic algorithm, such as cipher algorithm, key size, key purpose, operation mode, padding mode, hash mode, IV, Nonce, AAD, etc.

2. **(Optional)** Process data in segments [huks.updateSession()](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-updatesessionhukshandle-huksoptions)

    When processing large data (exceeding 100K) or when required by certain cryptographic algorithms, data needs to be processed in segments. Otherwise, this step can be skipped.

3. **(Mandatory)** Finalize the key session [huks.finishSession()](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-finishsessionhukshandle-huksoptions)

    Process the final segment of data and finalize the key session.

If any error occurs during the above stages or if the key operation is no longer needed, the session must be canceled [huks.abortSession()](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-abortsessionhukshandle-huksoptions) to terminate key usage.

> **Note:**
>
> For devices with limited memory, it is recommended that services split data according to the device's storage capacity and cyclically call [huks.initSession()](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-initsessionstring-huksoptions) and [huks.finishSession()](../../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md#func-finishsessionhukshandle-huksoptions) for processing.