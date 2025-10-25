# Introduction to Key Agreement and Algorithm Specifications  

In non-secure channel environments, a secure shared key can be negotiated without sharing any secrets by using key agreement algorithms.  

The following sections introduce the algorithms currently supported by the system and their corresponding specifications.  

## ECDH  

ECDH (Elliptic Curve Diffie–Hellman Key Exchange). The algorithm library framework provides ECDH capabilities for various elliptic curves.  

When creating a key agreement, the "String Parameter" column in the table must be used to specify the key agreement algorithm specification.  

| Asymmetric Key Algorithm | String Parameter | API Version |  
| :-------- | :-------- | :-------- |  
| ECC | ECC224 | 12+ |  
| ECC | ECC256 | 12+ |  
| ECC | ECC384 | 12+ |  
| ECC | ECC521 | 12+ |  
| ECC | ECC_BrainPoolP160r1 | 12+ |  
| ECC | ECC_BrainPoolP160t1 | 12+ |  
| ECC | ECC_BrainPoolP192r1 | 12+ |  
| ECC | ECC_BrainPoolP192t1 | 12+ |  
| ECC | ECC_BrainPoolP224r1 | 12+ |  
| ECC | ECC_BrainPoolP224t1 | 12+ |  
| ECC | ECC_BrainPoolP256r1 | 12+ |  
| ECC | ECC_BrainPoolP256t1 | 12+ |  
| ECC | ECC_BrainPoolP320r1 | 12+ |  
| ECC | ECC_BrainPoolP320t1 | 12+ |  
| ECC | ECC_BrainPoolP384r1 | 12+ |  
| ECC | ECC_BrainPoolP384t1 | 12+ |  
| ECC | ECC_BrainPoolP512r1 | 12+ |  
| ECC | ECC_BrainPoolP512t1 | 12+ |  
| ECC | ECC_Secp256k1 | 12+ |  
| ECC | ECC | 12+ |  

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the ECDH key agreement parameter supports omitting the specification of length and curve when inputting the key type. The key agreement operation depends on the actual input key.  

## X25519  

The algorithm library framework provides X25519 key agreement capabilities.  

When creating a key agreement, the "String Parameter" column in the table must be used to specify the key agreement algorithm specification.  

| Asymmetric Key Algorithm | String Parameter | API Version |  
| :-------- | :-------- | :-------- |  
| X25519 | X25519 | 12+ |  

## DH  

DH (Diffie–Hellman Key Exchange). The algorithm library framework provides DH key agreement capabilities.  

When creating a key agreement, the "String Parameter" column in the table must be used to specify the key agreement algorithm specification.  

| Asymmetric Key Algorithm | String Parameter | API Version |  
| :-------- | :-------- | :-------- |  
| DH | DH_modp1536 | 12+ |  
| DH | DH_modp2048 | 12+ |  
| DH | DH_modp3072 | 12+ |  
| DH | DH_modp4096 | 12+ |  
| DH | DH_modp6144 | 12+ |  
| DH | DH_modp8192 | 12+ |  
| DH | DH_ffdhe2048 | 12+ |  
| DH | DH_ffdhe3072 | 12+ |  
| DH | DH_ffdhe4096 | 12+ |  
| DH | DH_ffdhe6144 | 12+ |  
| DH | DH_ffdhe8192 | 12+ |  
| DH | DH | 12+ |  

As shown in the last row of the table, to maintain compatibility with keys generated from key parameters, the DH key agreement parameter supports omitting the specification of well-known safe prime groups when inputting the key type. The key agreement operation depends on the actual input key, and this scenario supports non-well-known group key agreement.