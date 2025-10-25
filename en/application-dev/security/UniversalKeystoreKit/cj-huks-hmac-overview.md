# Introduction to HMAC and Algorithm Specifications  

## Introduction to HMAC  

MAC (Message Authentication Code) provides a method for verifying the integrity of transmitted or stored information over unreliable media. HMAC (Hash-based Message Authentication Code) is a keyed-hash message authentication code that uses cryptographic hash functions and a secret key for message authentication. HMAC can be combined with any cryptographic hash function (e.g., MD5, SHA-1, etc.). HUKS supports HMAC in conjunction with mainstream digest algorithms.  

## Supported Algorithms  

The following are the specifications supported by HMAC.  

<!--Del-->  
For OpenHarmony, vendor-adapted key management service specifications are categorized into mandatory and optional specifications. Mandatory specifications are algorithm specifications supported by all vendors. For optional specifications, vendors decide whether to implement them based on actual circumstances. If needed, please refer to the specific vendor's documentation to ensure compatibility before use.  

**Developers are advised to use mandatory specifications for application development to ensure full platform compatibility.**  
<!--DelEnd-->  

| Digest Algorithm | Supported Key Length | API Level | <!--DelCol4-->Mandatory Specification |  
| :--------------- | :------------------- | :-------- | :------------------ |  
| <!--DelRow-->MD5, SHA1, SHA224 | 8 - 1024 | 15+ | No |  
| SHA256 | 192 - 1024 | 15+ | Yes |  
| SHA384, SHA512 | 256 - 1024 | 15+ | Yes |  
| SM3 | 8 - 4096 | 15+ | Yes |