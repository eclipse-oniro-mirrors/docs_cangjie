# Introduction to Encryption/Decryption and Algorithm Specifications  

In HUKS, when a key already exists, encryption or decryption operations on data can be performed using HUKS.  

## Supported Algorithms  

The following are the specifications for key encryption/decryption operations.  

<!--Del-->  
For OpenHarmony vendor adaptation, the Key Management Service specifications are divided into mandatory and optional specifications. Mandatory specifications are algorithm specifications that all vendors must support. For optional specifications, vendors decide whether to implement them based on actual circumstances. If you intend to use optional specifications, please refer to the specific vendor's documentation to ensure compatibility before use.  

**Developers are advised to use mandatory specifications for application development to ensure full platform compatibility.**  
<!--DelEnd-->  

### Standard Device Specifications  

| Algorithm/Block Mode/Padding Mode | Remarks | API Level | <!--DelCol4-->Mandatory Specification |  
| :-------- | :-------- | :-------- | :-------- |  
| <!--DelRow-->AES/ECB/NoPadding<br/>AES/ECB/PKCS7 | In ECB mode, if the padding mode is set to NoPadding, the plaintext data must be encrypted in fixed-length blocks. If the input data length is not a multiple of 16, the application must perform padding to meet the block length requirement. | 15+ | No |  
| AES/CBC/NoPadding<br/>AES/CBC/PKCS7<br/>AES/CTR/NoPadding | IV parameter is mandatory. In CBC mode, if the padding mode is set to NoPadding, the plaintext data must be encrypted in fixed-length blocks. If the input data length is not a multiple of 16, the application must perform padding to meet the block length requirement. | 15+ | Yes |  
| AES/GCM/NoPadding | Encryption: Nonce parameter is mandatory.<br/>Decryption: Nonce and TAG parameters are mandatory. | 15+ | Yes |  
| RSA/ECB/NoPadding<br/>RSA/ECB/PKCS1_V1_5<br/>RSA/ECB/OAEP | Supported digest algorithms for OAEP padding mode: SHA256/SHA384/SHA512. | 15+ | Yes |  
| <!--DelRow-->SM4/ECB/NoPadding<br/>SM4/ECB/PKCS7 | ECB mode is not recommended. | 15+ | No |  
| SM4/CBC/PKCS7 | IV parameter is mandatory. | 15+ | Yes |  
| SM4/CTR/NoPadding<br/>SM4/CBC/NoPadding<br/>SM4/CFB/NoPadding<br/>SM4/OFB/NoPadding | IV parameter is mandatory. | 12+ | Yes |  
| SM2/-/NoPadding | Digest algorithm: SM3. | 11+ | Yes |  
| DES/CBC/NoPadding<br/>DES/ECB/NoPadding | IV parameter is mandatory in CBC mode. | 15+ | Yes |  
| 3DES/CBC/NoPadding<br/>3DES/ECB/NoPadding | IV parameter is mandatory in CBC mode. | 15+ | Yes |  

### Lightweight Device Specifications  

<!--Del-->  
For the specifications listed for lightweight devices, OEM vendors will decide whether to implement them based on actual circumstances. If you intend to use these specifications, please refer to the specific vendor's documentation to ensure compatibility before use.  
<!--DelEnd-->  

| Algorithm/Block Mode/Padding Mode | Remarks | API Level |  
| :-------- | :-------- | :-------- |  
| AES/GCM/NoPadding | Encryption: Nonce parameter is mandatory.<br/>Decryption: Nonce and TAG parameters are mandatory. | 15+ |  
| AES/CBC/NoPadding<br/>AES/CTR/NoPadding | IV parameter is mandatory. | 15+ |  
| DES/ECB/NoPadding | - | 15+ |  
| DES/CBC/NoPadding | IV parameter is mandatory. | 15+ |  
| 3DES/ECB/NoPadding | - | 15+ |  
| 3DES/CBC/NoPadding | IV parameter is mandatory. | 15+ |  
| RSA/ECB/NoPadding | - | 15+ |  
| RSA/ECB/PKCS1_V1_5 | - | 15+ |  
| RSA/ECB/OAEP | Digest algorithm: SHA256. | 15+ |