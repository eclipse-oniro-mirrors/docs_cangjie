# Key Generation Introduction

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Key generation operations are commonly required in the following scenarios:

1. Randomly generating keys. The generated key object can be used for subsequent cryptographic operations such as encryption and decryption.

2. Generating keys from specified data (i.e., converting external or stored binary data into a key object). The generated key object can be used for subsequent cryptographic operations like encryption and decryption.

3. Extracting binary data from keys for storage or transmission purposes.

The key types include symmetric keys (SymKey) and asymmetric keys (public keys PubKey and private keys PriKey), where a public key and private key form a key pair (KeyPair).