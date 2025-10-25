# Introduction to Key Generation and Conversion  

The following scenarios frequently require key generation operations:  

1. Randomly generate a cryptographic library key object. This object can be used for subsequent operations such as encryption and decryption.  

2. Generate a cryptographic library key object based on specified data (i.e., converting external or stored binary data into a cryptographic library key object). This object can be used for subsequent operations such as encryption and decryption.  

3. Generate a specified cryptographic library key object based on key parameters. This object can be used for subsequent operations such as encryption and decryption.  

4. Obtain the binary data of a cryptographic library key object for storage or transmission.  

5. For asymmetric keys, obtain the parameter attributes of the key object for storage or transmission.  

Here, the key object `Key` includes symmetric keys (`SymKey`) and asymmetric keys (public key `PubKey` and private key `PriKey`), where the public and private keys together form a key pair (`KeyPair`).